Provide your CLI command here:
```bash
apt update && apt install curl jq -y && curl -X GET "https://example.com/api/$(jq -r 'select(.symbol == "TSLA" and .side == "sell") | .order_id' transaction-log.txt | paste -sd,)" -o output.txt
```