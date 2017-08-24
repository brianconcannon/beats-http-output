beats-http-output
=================

This is an http(s) output for Elastic beats. It allows for HTTP POSTs of collected events to an API. So far I have added the following features:

* Ability to specify HTTP headers
* Ability to microbatch events into a single POST. You can specify:
    * Batch size
    * Minimum time between POSTS
    * Maximum time between POSTS

Usage
=====

To use this output you have to clone the Elastic beats project: https://github.com/elastic/beats/tree/v5.5.1 and modify main.go by adding one
line importing this project.

```
package main

import (
	"os"

	_ "github.com/brianconcannon/beats-http-output"

    "github.com/elastic/beats/libbeat/beat"
	"github.com/elastic/beats/winlogbeat/beater"
)

var Name = "winlogbeat"

func main() {
	if err := beat.Run(Name, "", beater.New); err != nil {
		os.Exit(1)
	}
}
```

Then configure the http output plugin in winlogbeat.yml:

```
output:
  http:
    hosts: ["https://www.example.com:443/foo"]
    headers:
        Content-Type: application/json
        X-API-Key: abcdefghijklmnop...
```
