# libreelec-docker-deluge

Deluge for LibreELEC using Docker and systemd

## Comparison with other Deluge containers

* Doesn't compile some Deluge dependencies from source, resulting in drastically faster build times
* Same filesystem layout inside the container, meaning you can move a newly downloaded torrent to your library and 
continue seeding it. `/var/media` is mounted too so you can use symlinks to your other harddrives in `/storage`.
* The daemon accepts remote connections so you can use the GTK UI to manage Deluge
* Listen port exposed so you can become connectable
* Sane defaults for a good out of the box experience, you don't need to change anything unless you want to

## Requirements

* LibreELEC with the Docker addon installed

## Installation

### Building the image

* Download this repository as a ZIP file, then unpack it
* Run `./build.sh deluge x86_64` to build the Docker image. This will take about 5-10 minutes on your average Intel 
Celeron.
* Verify that the image got built by running `docker images | grep jalle19/libreelec-deluge`. You should see one 
tagged version and one "latest".

### Enabling the service

* Run `systemctl enable deluge.service`. If you make changes to this file later on you must also run 
`systemctl daemon-reload` for the changes to take effect.
* Run `systemctl start deluge` to start the service manually. The service will be automatically started during startup 
too.

## Settings

* The web interface is available on port 8112. The password to the interface is `deluge`.
* The daemon is listening for remote UI connections on port 58846. The username and password is `deluge`.
* Port 53160 (both TCP and UDP) is forwarded to the container so you can use port forwarding to become connectable

If you want to use the GTK UI to connect to the daemon you will have to create an additional user in Deluge. To do this, 
open `/storage/deluge/config/auth` and add a new line. See the Deluge documentation on how this file works.

### Customizing

If the setup doesn't suit your needs, just modify whatever you have to and follow the steps from the `Installation` 
section to rebuild the image and update the service.

## License

GNU General Public License 2.0
