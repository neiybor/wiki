<!-- TITLE: Deploy Environment Variables -->
<!-- SUBTITLE: How to add/remove/update environment variables -->

## Update `config-management`
1. Update the appropriate `config-management` files based on the environment (`development`, `staging`, or `production`) and repo (`frontend` or `backend`).
2. Follow the standard PR process to get your updated code onto the `master` branch.
3. Checkout/pull the `master` branch. Also, delete the local branch you used to create the PR. Let's keep our Git trees well-groomed. 🙂

## Update Heroku
4. Use the Heroku CLI to update Heroku. For each repo you want to update:
	5. `cd` into the corresponding directory (`frontend` or `backend`).
	6. Run `heroku config:push -f {{file name}} --app={{Heroku app name}}` for each environment you want to update.

Here are some example commands that might be run to update the env vars in Heroku:
`cd frontend/
heroku config:push -f .env.staging.frontend --app=neiybor-frontend-staging`

`cd backend/
heroku config:push -f .env.production.backend --app=neighbor-api`