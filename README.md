beats-http-output
=================

[![Build Status](https://travis-ci.org/brianconcannon/beats-http-output.svg?branch=master)](https://travis-ci.org/brianconcannon/beats-http-output)

This is an http(s) output for Elastic beats. There are other similar projects, such as https://github.com/raboof/beats-output-http. In this project I've added the ability to specify http headers in the config and will likely add other features down the road.

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
