## Usage

go get github.com/toomasp/influxdb1-client

## Example
The following example creates a new client to the InfluxDB host on localhost:8086 and runs a query for the measurement `cpu_load` from the `mydb` database. 
``` go
func ExampleClient_query() {
	c, err := client.NewHTTPClient(client.HTTPConfig{
		Addr: "http://localhost:8086",
	})
	if err != nil {
		fmt.Println("Error creating InfluxDB Client: ", err.Error())
	}
	defer c.Close()

	q := client.NewQuery("SELECT count(value) FROM cpu_load", "mydb", "")
	if response, err := c.Query(q); err == nil && response.Error() == nil {
		fmt.Println(response.Results)
	}
}
```
