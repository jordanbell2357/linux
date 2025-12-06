# Random.org

<https://www.random.org/>

<https://api.random.org/json-rpc/4/basic#generateStrings>

We make request.json:

```json
{
    "jsonrpc": "2.0",
    "method": "generateStrings",
    "params": {
        "apiKey": "<API Key>",
        "n": 10,
        "length": 4,
        "characters": "abcdefghijklmnopqrstuvwxyz",
        "replacement": true,
        "pregeneratedRandomization": null
    },
    "id": 11359
}
```

The API URL is `https://api.random.org/json-rpc/4/invoke`

<https://curl.se/docs/manpage.html>

> If you start the data with the letter @, the rest should be a filename to read the data from, or - if you want curl to read the data from stdin. Posting data from a file named 'foobar' would thus be done with --data @foobar. When --data is told to read from a file like that, carriage returns, newlines and null bytes are stripped out. If you do not want the @ character to have a special interpretation use --data-raw instead.

```bash
curl -s -X POST https://api.random.org/json-rpc/4/invoke -H "Content-Type: application/json" -d @request.json > response.json
```

We use jq to inspect response.json. [^jq]

[^jq]: <https://www.linode.com/docs/guides/using-jq-to-process-json-on-the-command-line/>

```bash
jq '.' response.json
```

```json
{
  "jsonrpc": "2.0",
  "result": {
    "random": {
      "data": [
        "mywj",
        "rlkk",
        "hhng",
        "iqua",
        "hwqx",
        "fedb",
        "bplh",
        "etxs",
        "oosk",
        "wkac"
      ],
      "completionTime": "2025-12-06 18:20:18Z"
    },
    "bitsUsed": 188,
    "bitsLeft": 249436,
    "requestsLeft": 997,
    "advisoryDelay": 580
  },
  "id": 11359
}
```

```console
jq '.result.random.data' response.json
```

```console
[
  "mywj",
  "rlkk",
  "hhng",
  "iqua",
  "hwqx",
  "fedb",
  "bplh",
  "etxs",
  "oosk",
  "wkac"
]
```


```bash
jq '.result.random.data[0]' response.json
```

```console
"mywj"
```
