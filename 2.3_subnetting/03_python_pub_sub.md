# 6. Connect to EMQX Cloud using Python

We will now use Python to publish and receive MQTT messages through your EMQX Cloud broker.

We will create two Python programs:
- A publisher that sends two messages.
- A subscriber that listens for messages and displays them.

## 6.1 Install dependencies

Open the Raspberry Pi terminal and install the Paho MQTT library:

```bash
pip install paho-mqtt
```

Make sure your Python virtual environment is activated if you created one in the previous activity.

## 6.2 Publish two messages

The following Python program publishes two messages to the same MQTT topic:

- `test 1` under the topic `my test`
- `test 2` under the topic `my test`

Create a Python file:

```bash
nano my_publisher.py
```

Copy and paste the following code:

```python
import ssl
import paho.mqtt.client as paho
import paho.mqtt.publish as publish

# Create two test messages
msgs = [
    {'topic': "my test", 'payload': "test 1"},
    {'topic': "my test", 'payload': "test 2"}
]

# Use TLS for a secure connection with EMQX Cloud
sslSettings = ssl.create_default_context(
    cafile="emqxsl-ca.crt"
)

# Enter your EMQX Cloud credentials
auth = {
    'username': "USERNAME",
    'password': "PASSWORD"
}

# Publish both messages
publish.multiple(
    msgs,
    hostname="HOSTNAME",
    port=8883,
    auth=auth,
    tls=sslSettings,
    protocol=paho.MQTTv311
)

print("Messages published successfully!")
```

Replace the following values with your own details:

- `USERNAME`: Your EMQX Cloud username.
- `PASSWORD`: Your EMQX Cloud password.
- `HOSTNAME`: Your EMQX Cloud broker hostname.
- `emqxsl-ca.crt`: The filename of your downloaded EMQX CA certificate.

Save the file and execute it:

```bash
python my_publisher.py
```

The program should connect to EMQX Cloud and publish both messages.

## 6.3 Subscribe to MQTT messages

Now we will create a second Python program to receive messages from the broker.

Create another file:

```bash
nano my_subscriber.py
```

Copy and paste the following code:

```python
import ssl
import paho.mqtt.client as paho
import paho.mqtt.subscribe as subscribe

# Callback function to print incoming messages
def print_msg(client, userdata, message):
    print(
        "{} : {}".format(
            message.topic,
            message.payload.decode()
        )
    )

# Use TLS for a secure connection with EMQX Cloud
sslSettings = ssl.create_default_context(
    cafile="emqxsl-ca.crt"
)

# Enter your EMQX Cloud credentials
auth = {
    'username': "USERNAME",
    'password': "PASSWORD"
}

# Subscribe to the topic
try:
    subscribe.callback(
        print_msg,
        "my test",
        hostname="HOSTNAME",
        port=8883,
        auth=auth,
        tls=sslSettings,
        protocol=paho.MQTTv311
    )

except KeyboardInterrupt:
    print("\nSubscriber stopped.")
```

Again, replace the username, password, hostname and certificate filename with your own details.

Save the file.

## 6.4 Test your MQTT communication

Now let's test the two programs.

**Step 1 – Start the subscriber**

Open a terminal and execute:

```bash
python my_subscriber.py
```

Leave this terminal open. The program will connect to EMQX Cloud and wait for incoming messages.

**Step 2 – Run the publisher**

Open a second terminal and execute:

```bash
python my_publisher.py
```

**Step 3 – Observe the results**

Return to the first terminal.

You should see the following output:

```text
my test : test 1
my test : test 2
```

Congratulations! You have successfully published and received MQTT messages using Python and EMQX Cloud.

> **Insert Screenshot 6:** Both terminals showing the publisher and subscriber working successfully.

## 6.5 Experiment

Try modifying the publisher to send different messages:

```python
msgs = [
    {'topic': "my test", 'payload': "Temperature: 22.5"},
    {'topic': "my test", 'payload': "Humidity: 65%"}
]
```

Run the publisher again and observe the subscriber.

You can also change the topic from `my test` to:

```text
university/temperature
```

Remember to update the topic in both programs.

