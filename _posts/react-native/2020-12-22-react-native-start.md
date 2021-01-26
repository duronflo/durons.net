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
{% raw  %}

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
{% endraw  %}
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



### Flatlists und Sectionlists.

Beispiel für eine SectionList:

{% highlight javascript linenos %}
{% raw  %}

import React, {Component} from 'react';
import { SectionList, StyleSheet, Text, View } from 'react-native';


export default class SettingScreen extends Component<any, any> {
    render() {
        return (
            <View style={styles.container}>
                <SectionList
                    // data=
                    sections={
                        [
                            {
                                title: 'Version',
                                data: [{key: 1, info: '1.0'}]
                            },
                            {
                                title: 'Impressum',
                                data: [
                                    {key: 3, info: 'flo@durons.net'},
                                    {key: 4, info: 'Copyright 2021'},
                                ]
                            }
                        ]
                    }
                    renderItem={({item}) => <Text style={styles.item}>{item.info}</Text>}
                    renderSectionHeader={({section}) =>
                        <Text style={styles.section}>{section.title}</Text>}


                />


            </View>
        );
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#e6e6ea',
        paddingTop: 30
    },
    section: {
        backgroundColor: 'whitesmoke',
        borderWidth: StyleSheet.hairlineWidth,
        borderColor: 'lightgrey',
        fontSize: 18,
        padding: 5
    },
    item: {
        color: 'dimgrey',
        fontSize: 18,
        padding: 5
    }
});

{% endraw  %}
{% endhighlight %}

Wichtige Links:

Dokumentation von FlatList: [reactnative.dev/docs/flatlist](reactnative.dev/docs/flatlist)

Dokumentation von SectionList: [reactnative.dev/docs/sectionlist](reactnative.dev/docs/sectionlist)

### Weitere nützliche Widgets

#### Touchables - Elegantere Darstellung von Buttons
Beschreibung der Touchable-Komponenten: [reactnative.dev/docs/handling-touches](reactnative.dev/docs/handling-touches)

Dokumentation zu TouchableOpacity: [reactnative.dev/docs/touchableopacity](reactnative.dev/docs/touchableopacity)

#### Allgemeines Infos zur Image Komponente

Allgemeines zur Image-Komponente: [reactnative.dev/docs/images](reactnative.dev/docs/images)


#### ScrollView 

ScrollView sollte nur für kurze "Scrolls" verwendet werden. Für lange Scrolls immer FlatList oder SectionList verwenden.

Dokumentation zu ScrollView: [reactnative.dev/docs/scrollview](reactnative.dev/docs/scrollview)

#### Dimensions API - Abragen der Screengröße des entsprechenden Zielgeräts

Dokumentation zur Dimensions-API: [https://reactnative.dev/docs/dimensions](https://reactnative.dev/docs/dimensions)

Beispielweise kann man auch die aktuelle Screengröße des Zielgeräts abfragen:

{% highlight javascript linenos %}
{% raw  %}
const width = Dimensions.get('window').width * 0.5;
{% endraw  %}
{% endhighlight %
