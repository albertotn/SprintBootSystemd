# SprintBootSystemd

A systemd definition for sprint boot based application

## Description

After develop an application with spring boot you get a runnable jar and make it working on a remote server to provide your service is a must. In order to do so in linux, you have to create a service . There are a lot of different options and I've decided to provide a [Systemd](https://en.wikipedia.org/wiki/Systemd) definition.

I've tested this setup on Centos 7 ( on an aws ec2 machine ) and works fine for my goal, so feel free to use it and personalize it


	[Unit]
	# General information
	Description=your description
	After=network.target

	[Service]
	WorkingDirectory=/yourdir
	# Spring boot starting command
	ExecStart=/bin/java -jar yourjar.jar
	# Path of file containing the env vars used by application
	EnvironmentFile=/path/to/.env
	
	# Send an exit code
	SuccessExitStatus=143
	TimeoutStopSec=10

	# Location for logging files
	StandardOutput=file:/var/log/service-output.log
	StandardError=file:/var/log/service-error.log

	Restart=on-failure
	RestartSec=5s

	[Install]
	WantedBy=multi-user.target

## Installation

1. Copy your `myservice.service` into folder `/etc/systemd/system`
2. Let systemd know new stuff with `sudo systemctl daemon-reload`
3. Enable the service with `sudo systemctl enable myservice.service`
4. Start the service with `sudo systemctl start myservice.service`

## Limitations

This systemd is only a starting point, some possibile personalizations:

- avoid to redirect service's standard output and error to journal and put on a log file
- personalize restart policy

# License

See LICENSE file


