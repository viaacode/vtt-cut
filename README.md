# vtt-cut
Microservice that cuts a VTT subtitle file between a certain start and end time

## General
This serice listens to a RabbitMQ queue and will transform and publish the XIF posted as 'data' to the WebVTT format along with the correlation id originally sent with the request.

## Usage
Publish a message with the following format on the request queue:
```
{
    "start": "10000800",
    "end": "10002923",
    "correlationid": "correlationdid0",
    "data": "&lt;XIF version=&quot;1.0&quot;&gt;&lt;/XIF&gt;"
}
```
The start and end format must match the following format (without the colons):

> 10:00:08:00

Where the numbers are: hours, minutes, seconds and hundreths of a second respectively.

The response will be posted on the response queue using the following format:
```
{
	"correlationid": "correlationid0",
	"data": "&lt;XIF version=&quot;1.0&quot;&gt;&lt;/XIF&gt;"
}
```
