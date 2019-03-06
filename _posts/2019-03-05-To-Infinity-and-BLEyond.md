---
layout: post
title:  "To Infinity and BLEyond"
date:   2019-03-04 22:33:00 -0600
categories: BLE, Coding
---

## Making an IOT device

# Overview

This post starts with an overview of BLE (Bluetooth Low Energy) and finishes with an overview of a very basic BLE application. 

# BLE Basics

BLE (Bluetooth Low Energy) is a protocol designed for devices that need to transmit information intermittenly that need to preserve battery life.

Any bluetooth device uses services and characteristics. It's probably easier to start with identifying a characteristic; It is an item that contains value. This can be anything from a direction of wind to an a devices power level. A service is a collection of characteristics that serve a unified purpose. 

Services and charateristics belong to the GATT (Generic Attributes) paradigm. Another important concept of BLE is GAP (Generic Access Profile), which defines how a connection is initiated betwen BLE devices. A typical example, has one device called a peripheral and another called a central. The peripheral periodically advertises a service it has. Essentially, the peripheral is saying 'here I am this is what I do' so other devices can hear it. The central listens for those devices, and connects when there is one that performs the serice the central wants. 


# The BLE Application

I programmed an IOS app, and a microcontroller to create a BLE connection. For the microcontroller I used an Adafruit Huzzah ESP32. 

The microcontroller is connected to 3 LED's (green, yellow, and red), and a switch. The IOS app has three buttons (green, yellow, and red), and a counter. If you press the red button, the red light turns on. The yellow, the yellow and green green. Only one light will be on at a time. If you press the switch on the microcontroller, the counter will increase by one. 

# Programming a BLE enabled microcontroller 

The microcontroller is the peripheral, and advertises a random service. 

> A service is a number being broadcast called a UUID. There are many typical service UUID's if you have a typical application purpose, but if its not then you need your own. You can generate the on some website just look up `UUID Generator` and you'll find it. 

In the service there are two characteristics. One for the lights, and one for the switch. The service is advertised for all to see. 

[Code for the ESP32](https://github.com/njdullea/ble_connection_example/blob/master/ble_2Characs_ESP32/ble_2Characs/ble_2Characs.ino)

# Programming an IOS application to support BLE

IOS uses a library called `CoreBluetooth` for, you guessed it, bluetooth. 

The app searches for the same service the microcontroller is advertising. The app initiates connections, and request updates from the switch characteristic, and can write to the light characteristic when a color button is pressed. 

The biggest pain point was figuring out how to write the information that is passed over BLE. What I ended up doing, was assining numbers (1, 2, 3) to each of the buttons because that is much easier to encode into Swift's data (bytes) to be sent over the BLE connection, and easy to translate back. 

[Code for the IOS app](https://github.com/njdullea/ble_connection_example/blob/master/ble_2Charac_IOS/ble_example/ble.swift)


Thanks for checking this out. 

I'm up, up, and outta here!