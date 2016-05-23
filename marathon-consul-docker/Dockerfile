FROM ubuntu:14.04

RUN apt-get update && \
	dpkg --list | awk '{print $2}' | sort > /tmp/package-list-before.txt && \
    apt-get install -y curl && \
    dpkg --list | awk '{print $2}' | sort > /tmp/package-list-after.txt && \
	curl -s https://bintray.com/user/downloadSubjectPublicKey?username=allegro | sudo apt-key add - && \
	apt-get purge -y `comm -1 -3 /tmp/package-list-before.txt /tmp/package-list-after.txt` && \
	rm -rf /tmp/package-list-before.txt /tmp/package-list-after.txt && \
    echo "deb http://dl.bintray.com/v1/content/allegro/deb /" | sudo tee /etc/apt/sources.list.d/marathon-consul.list && \
	sudo apt-get -y update && \
	sudo apt-get --force-yes -qy install marathon-consul && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

CMD marathon-consul --marathon-location=192.168.99.100:8080 --sync-interval=5m --log-level=debug
