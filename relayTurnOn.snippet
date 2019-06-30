#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import configparser
import paho.mqtt.client as mqtt
from hermes_python.hermes import Hermes
from hermes_python.ffi.utils import MqttOptions
from hermes_python.ontology import *
import io

client = mqtt.Client("voiceCnt_test0")
CONFIGURATION_ENCODING_FORMAT = "utf-8"
CONFIG_INI = "config.ini"

class SnipsConfigParser(configparser.SafeConfigParser):
    def to_dict(self):
        return {section : {option_name : option for option_name, option in self.items(section)} for section in self.sections()}


def read_configuration_file(configuration_file):
    try:
        with io.open(configuration_file, encoding=CONFIGURATION_ENCODING_FORMAT) as f:
            conf_parser = SnipsConfigParser()
            conf_parser.readfp(f)
            return conf_parser.to_dict()
    except (IOError, configparser.Error) as e:
        return dict()

def subscribe_intent_callback(hermes, intentMessage):
    conf = read_configuration_file(CONFIG_INI)
    action_wrapper(hermes, intentMessage, conf)


def action_wrapper(hermes, intentMessage, conf):
    """ Write the body of the function that will be executed once the intent is recognized.
    In your scope, you have the following objects :
    - intentMessage : an object that represents the recognized intent
    - hermes : an object with methods to communicate with the MQTT bus following the hermes protocol.
    - conf : a dictionary that holds the skills parameters you defined.
      To access global parameters use conf['global']['parameterName']. For end-user parameters use conf['secret']['parameterName']

    Refer to the documentation for further details.
    """

    if len(intentMessage.slots.house_room) > 0:
        house_room = intentMessage.slots.house_room.first().value # We extract the value from the slot "house_room"
        result_sentence = ""  # The response that will be said out loud by the TTS engine.
        device_name = intentMessage.slots.device.first().value
        action_performed = False

        if house_room == "living room":
            if device_name == "LED strip":
                client.publish("cmnd/tv_light_status/POWER","ON")
                action_performed = True
        elif house_room == "kitchen":
            if device_name == "LED strip":
                client.publish("cmnd/k_light_status/POWER","ON")
                action_performed = True
        if action_performed:
            result_sentence = "Turning on {} in {}".format(str(device_name), str(house_room))
        else:
            result_sentence = "No {} found in {}".format(str(device_name), str(house_room))
    else:
        result_sentence = "No light source detected"

    current_session_id = intentMessage.session_id
    hermes.publish_end_session(current_session_id, result_sentence)



if __name__ == "__main__":
    mqtt_opts = MqttOptions()
    client.connect("192.168.1.72")
    with Hermes(mqtt_options=mqtt_opts) as h:
        h.subscribe_intent("relayTurnOn", subscribe_intent_callback) \
         .start()