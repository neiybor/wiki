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

1. get the reservation_id for the reservation you wish to discount (<R_ID>)
2. modify the neighbor fee for future payments:
	1. `select value from reservation_metadata where reservation_id=<R_ID> and key='fees';` # gets the value of the fees
	2. modify the fees value like so '[{"fee":"neighbor","amt":4215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' => '[{"fee":"neighbor","amt":2215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' (this is for a $20 discount)
	3. `update reservation_metadata set value='[{"fee":"neighbor","amt":2215},{"fee":"stripe","amt":1614},{"fee":"host","amt":26486}]' where reservation_id=<R_ID> and key='fees';`

