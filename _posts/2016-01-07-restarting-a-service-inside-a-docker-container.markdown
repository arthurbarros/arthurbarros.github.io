---
published: true
title: Restarting a service inside a docker container
layout: post
author: Arthur Barros
---

I have this project running on a container with apache_wsgi + flask, and I hadn't set up the WSGIScriptReloading yet, and I was wondering if was possible to send a SIGKILL to a service inside a container without manually attach to the container and run it by myself.

And thanks to the amazing work of the docker community, it's actually possible to send a SIGKILL using the `docker kill` command, here is how:

    docker kill --signal="USR1" container_name_here

That's it, you can send any SIGKILL you want to the service running in the container, ofcourse it depends if the service support some or any of the POSIX SIGKILL

Here is some working SIGKILL for apache if you are wondering.

    TERM - Stop Now Signal
    USR1 - Graceful Restart Signal
    HUP - Restart Now Signal
    WINCH - Graceful Stop Signal
 
You can read more about the `--signal` flag here [https://docs.docker.com/engine/reference/commandline/kill/](https://docs.docker.com/engine/reference/commandline/kill/)


# Post Update about the PID 1

Is important to mention that your process inside the container MUST be running with PID 1, in other words, It should be the process you expose with ENTRYPOINT/CMD, if you are running your main process with a bash bias. This will not work

