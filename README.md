Requirements:
These files are an adaptation to Professor Kutzer's OptiTrack toolbox:
https://www.mathworks.com/matlabcentral/fileexchange/55675-kutzer-optitracktoolbox

Requires Python 3
https://www.python.org/downloads/

1. Add paho-mqtt Python library
    - https://pypi.org/project/paho-mqtt/
    - Windows commandline:
    - pip install paho-mqtt
        - If this fails due to self-signed certs, see the instructions in 'pip' folder in this repository.

2. Replace 'OptiTrack.m' in Professor Kutzer's Matlab toolbox (file location varies by install and machine)
    - Make sure it's the active install directory, not the Downloaded / unzipped directory.
    - something like C:\Program Files\MATLAB\*[Matlab Version]*\toolbox\optitrack

3. Add 'callback.py' to the same folder as 'OptiTrack.m'
    - This file shall be editable by [student,faculty,whoever] and will ideally be customized for application.
    - Presently just prints out the result of subscription.
    - As the filename implies, MQTT subscriptions are interrupt driven to a callback function.
    - If editing this file, be mindful of Matlab rules for reloading python modules.

4. Run Matlab as admin.

Usage in Matlab:
- **opti=OptiTrack**
- *no Initialization needed, connects unicast at instantiation*
- **opti.RigidBody**
    - With motion capture system running and a Rigid Body, should see feedback

MQTT publishing:
- **opti.publish(sample rate = 50 Hz, nsamples = infinite, MQTT broker = opti.defaultserver)**
- if nsamples == 0, runs in infinite while loop.

MQTT subscribing:
- **opti.subscribe(topic='test', MQTT broker = opti.defaultserver)**
    - When a subscribed topic has an incoming message, the OptiTrack.m outsources the handling to the singular function in callback.py

**opti.stopMQTT()** will stop the MQTT services by resetting the MQTT object.

**opti.defaultserver** is set to the OptiTrack server, but can be changed to another IP.

Once either publish() or subscribe() are issued, the IP of the MQTT broker cannot be changed except after running stopMQTT().
- The Broker IP is same for both subscription and publish.
- The MQTT object can only connect to 1 broker at a time.
- The IP of the broker can be checked, or manually set, via **opti.mqtt_server**
- It is possible to instantiate multiple MQTT objects, with separate broker IPs and/or callbacks, but that functionality is not presently built into this implementation.

# Optitrack
Development of OptiTrack lab

Todo:
- Add MQTT broker to startup routine of Optitrack box?
- Get RasPi on WiFi
- RasPi: repeat all the wired tests on wireless.
- Possibility of creating a WRCE Labs local Admin account (?)
    - I doubt this is possible, but at least want to ask
- Update Motive (?)
    - V3 will become available soon
    - Need updated license
- Google Drive ??

Done:
- Cloned HD; installed in bay of OptiTrack box. Not connected.
- Unicast working before joined
- Migrate data out of user OptiTrack's "Documents" to "C:/OptiTrack"
- Joined on network
- Test Unicast after joined to local, remote wired, and wireless
- Test MQTT after joined to local, remote wired, and wireless
- RasPi (wired) comms on MQTT
- RasPi (wired) update OS
- RasPi (wired) pip/pip3 works
    - requires work around for certs:
        curl apt.cs.usna.edu/ssl/install-ssl-system.sh | bash
- RasPi (wired) ssh and VNC
- gained local Admin on OptiTrack box
    - Each user will have to request this (?)
- Installed associated software on OptiTrack server
- OptiTrack server runs Matlab and MQTT broker

