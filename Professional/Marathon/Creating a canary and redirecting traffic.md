- Create the canary with the following command
	- `scripts/deploy-marathon-apps-to-production.sh -c -v VERSION NUMBER app_name-canary`
- Redirect traffic to that canary
	- `scripts/update-envoy-canary-routing.sh -e production /app_name 90 10`
		- where `90` is on production and `10` is the canary and `-e` is the environment
		  