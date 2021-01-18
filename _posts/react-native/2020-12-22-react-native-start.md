---
title: Erste Schritte mit dem App-Framework React native
permalink: /technology/react-native/first-steps-react-native
categories: [App-Development]
tags: [JavaScript, Node, Android, IPhone]
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
