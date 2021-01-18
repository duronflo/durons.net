---
title: Erste Schritte mit dem App-Framework React native
permalink: /technology/react-native/first-steps-react-native
categories:
  - App-Development
tags:
  - JavaScript
  - Node
  - Android
  - IPhone
  - ReactNative
technology: react-native
classes: wide
---

## Der Anfang mit React Native

## Wichtige Links bzw. Dateien

![](/assets/images/react-native-lifecycle.png)


https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/

## Flex-Box - Flexible und dynamische Gestaltung von Widgets in Apps

Codesnippet:
{% highlight javascript linenos %}

    import {StatusBar} from 'expo-status-bar';
    import React, {Component} from 'react';
    import {StyleSheet, View} from 'react-native';

    export default class App extends Component {
        render() {
            return (
                <View style={styles.container}>
                    <View style={[styles.box, {backgroundColor: 'cyan'}]}/>
                    <View style={[styles.box, {backgroundColor: 'green', alignSelf: 'flex-start'}]}/>
                    <View style={[styles.box, {backgroundColor: 'red'}]}/>
                </View>
            );
        }
    }

    const styles = StyleSheet.create({
        container: {
            flex: 1,                            // flex > 0 --> MAXIMALE Ausdehnung/Größe
            flexDirection: "column",               // Aurichtung der Hauptachse --> Zeile
            justifyContent: "center",     // Anordnung auf der Hauptachse
            alignItems: "center"                // Anordung auf der Querachse (entgegen der Hauptachse)
        },
        box: {
            width: 100,
            height: 100
        }
    });
{% endhighlight %}

## Navigation mit verschiedenen Möglichkeiten (Beispiel: BottomTabs)

Strukturierung in AppNavigator Klasse zur übersichtlichen Erzeugen von Tab-Strukuren.


{% highlight javascript linenos %}
{% raw  %}

import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import { NavigationContainer} from "@react-navigation/native";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import * as Icon from '@expo/vector-icons'

/* Screens have been outsourced*/
import FriendScreen from "./screens/FriendScreen";
import SettingScreen from "./screens/SettingScreen";

const Tab = createBottomTabNavigator();


export default function AppNavigator() {
    return (
        <NavigationContainer>
            <Tab.Navigator

                screenOptions={ ({route}) => {
                    return {
                        tabBarIcon: ({focused, size, color}) => {

                            let icon = '';
                            // route 'Home' --> home
                            if (route.name === 'Home')
                                icon = focused ? 'home' : 'home-outline';
                            // route 'Settings' --> settings
                            else if (route.name === 'Settings')
                                icon = focused ? 'settings' : 'settings-outline';
                            else
                                icon = '';

                            return (
                                <Icon.Ionicons
                                    // @ts-ignore
                                    name={icon}
                                    size={size}
                                    color={color}
                                />
                            );
                        },
                    };
                }
                }
                tabBarOptions={{
                    activeTintColor: 'orange',
                    style: {backgroundColor: 'aliceblue'},
                }}

                >
                <Tab.Screen
                    name='Home'
                    component={FriendScreen}
                    options={{
                        title: 'Home'

                    }}
                />
                <Tab.Screen
                    name='Settings'
                    component={SettingScreen}
                    options={{
                        title: 'Einstellungen'

                    }}
                />
            </Tab.Navigator>
        </NavigationContainer>
    );
}

{% endraw  %}
{% endhighlight %}
