# SprintBootSystemd

A systemd definition for sprint boot based application

## Description

After develop an application with spring boot you get a runnable jar and make it working on a remote server to provide your service is a must. In order to do so in lunux, you have to create a service . There are a lot of different options and I've decided to provide a [Systemd](https://en.wikipedia.org/wiki/Systemd) definition.

I've tested this setup on Centos 7 ( on an aws ec2 machine ) and works fine for my goal, so feel free to use it and personalize it


	[Unit]

	Description=your description
	After=network.target

	[Service]
	WorkingDirectory=/yourdir

	ExecStart=/bin/java -jar yourjar.jar

	SuccessExitStatus=143
	TimeoutStopSec=10

	StandardOutput=file:/var/log/service-output.log
	StandardError=file:/var/log/service-error.log

	Restart=on-failure
	RestartSec=5s

	[Install]
	WantedBy=multi-user.target

## Limitations

This systemd is only a starting point, some possibile personalizations:

- avoid to redirect service's standard output and error to journal and put on a log file
- personalize restart policy

# License

See LICENSE file


