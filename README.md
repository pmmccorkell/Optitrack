Requirements:
These files are an adaptation to Professor Kutzer's OptiTrack toolbox:
https://www.mathworks.com/matlabcentral/fileexchange/55675-kutzer-optitracktoolbox

Requires Python 3
https://www.python.org/downloads/

1. Add paho-mqtt Python library
    - https://pypi.org/project/paho-mqtt/
    - Windows commandline:
    - pip install paho-mqtt

2. Replace 'OptiTrack.m' in Professor Kutzer's Matlab toolbox (file location varies by install and machine)
    - Make sure it's the active install directory.

3. Add 'callback.py' to the same folder as 'OptiTrack.m'
    - This file shall be editable by [student,faculty,whoever] and will ideally be customized for application.
    - Presently just prints out the result of subscription.
    - As the filename implies, MQTT subscriptions are interrupt driven to a callback function.

Usage in Matlab:
- opti=OptiTrack
- *no Initialization needed, connects unicast at instantiation*
- opti.RigidBody      # With motion capture system running and a Rigid Body, should see feedback

MQTT publishing:
- **opti.publish(sample rate = 50 Hz, # samples = infinite, MQTT broker = '127.0.0.1')**

MQTT subscribing:
- **opti.subscribe(topic='test', MQTT broker = '127.0.0.1')**
    - When a subscribed topic has an incoming message, the OptiTrack.m outsources the handling to the singular function in callback.py

**opti.stop()** will stop the MQTT services by resetting the MQTT object.

Once either publish() or subscribe() are issued, the IP of the MQTT broker cannot be changed except after running stop().
- The MQTT object can only make 1 connection. 
- It is possible to instantiate multiple MQTT objects, with separate broker IPs and/or callbacks, but that functionality is not presently built into this implementation.
- Also be mindful of 

# Optitrack
Development of OptiTrack lab

Done:
- Cloned HD. Cloned HD installed in OptiTrack box; not connected.
- Unicast working before joined
- Joined on network
- Migrate data out of user OptiTrack's "Documents" to "C:/OptiTrack"
- Test Unicast after joined to local, remote wired, and wireless
- Test MQTT after joined to local, remote wired, and wireless
- RasPi (wired) comms on MQTT
- RasPi (wired) update OS
- RasPi (wired) pip/pip3 works
    - requires work around for certs:
        curl apt.cs.usna.edu/ssl/install-ssl-system.sh | bash
- RasPi (wired) ssh and VNC

Todo:
- Submitted ticket for admin on Optitrack 12/31
- Get RasPi on WiFi
- RasPi: repeat all the wired tests on wireless.
- Google Drive ??

      
