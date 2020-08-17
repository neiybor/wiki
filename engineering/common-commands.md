<!-- TITLE: Common Commands -->
<!-- SUBTITLE: Some common commands I always forget -->

# Header
**Start dev environment** `start`
* **Start rails server individually** `rails s -p 3001`
* **Start react server individually** `yarn start`
* **Start localstack individually** ?

**Run tests locally** `yarn test`
* **Run headless tests** `REACT_APP_TEST_HEADLESS=true yarn test`

**Debug rails in the console** `rails c`

**Run DB pending migrations** `rails db:migrate`

**Access dev DB** `devdb`

## discounting reservations through reducing neighbor fee
a common request from CS is to ask us to discount a reservation for various reasons. the main way we can do this is to do so via the neighbor fee. this section documents the process of things to be aware of when doing such a thing.

**background:** the way the payments for Neighbor work is that we process a payment from the renter to Neighbor on the first day (recorded in the `payments` table). We then create future transfers against that payment to the Host and to Neighbor (and eventually to Stripe?). those transfers are recorded in the `transfers` table with a future `schedued_transfer_date`. this means that in order to capture a change in what is going to be charged and transfered, you must look in multiple places.

1. get the reservation_id for the reservation you wish to discount (<R_ID>)
2. modify the neighbor fee for future payments:
	1. `select id,value from reservation_metadata where reservation_id=<R_ID> and key='fees';` # gets the value of the fees. the returned is is <M_ID>
	2. modify the fees value like so '[{"fee":"neighbor","amt":4215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' => '[{"fee":"neighbor","amt":2215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' (this is for a $20 discount)
	3. `update reservation_metadata set value='[{"fee":"neighbor","amt":2215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' where id=<MD_ID>;`
3. check existing payments:
	1. `select user_id, total, service_fee, payment_date, paid, failed, paid_period_start_date from payments where reservation_id=8185;`
		1. for future payments, get the `id` of the payment (<P_ID>). we should not be issuing transfer reductions on transfers for payments that have already been paid. we'll need to find a better way to take care of that situation.
		2. calculate the dollars off price from both the `total` and `service_fee` fields. in our example i'm using an original total fee of $323.14 and a service_fee of $42.15. the adjusted will be total=$304.15 and service_fee=$23.15.
		3. `update payments set total=304.15,service_fee=23.15 where id=<P_ID>;`
4. modify the pending transfers
	1. `select * from transfers where payment_id=<P_ID>;`
	  1. this will show us the various transfers associated with a payment. there should at least be one transfer to `destination_user_id` associated with Neighbor. it will usually be a smaller amount and as of the time of this writing the user_id is 1182 (Neighbor Ops).
	2. get the id associated with the transfer described above (<T_ID>) and get the reduced dollar amount you need to set it to. in our example we are going from a Neighbor fee of $42.15 to a Neighbor fee of $22.15.
	3. `update transfers set transfer_amount=22.15 where id=<T_ID>;`