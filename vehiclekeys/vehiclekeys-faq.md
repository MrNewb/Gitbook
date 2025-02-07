---
icon: newspaper
---

# FAQ



## Why is the car still on when I get out?

{% hint style="success" %}
Vehicles will remain on when getting out of them, this is an intended feature that adds to immersion.&#x20;



Most huds feature an engine toggle that you can use to turn the vehicle off before exiting or with the keyfob. If you dont have this option I have included an optional one.
{% endhint %}

{% hint style="success" %}
How do I make my script work with keys?



If you are running into issues on compatibility please make a ticket in the discord and we will try to help. The exports are also available on this documentation page.
{% endhint %}

{% hint style="success" %}
Why do my keys say null when spawning my car?&#x20;



This is because you need to add the text entry for the vehicles based on model. (hit z while in a custom car that does that and you will see the name isn't provided in game).
{% endhint %}

{% hint style="success" %}
Do lockpicks work?&#x20;



Yes, these are registered as usable items located in the framework bridge for "lockpick" and "advancedlockpick".
{% endhint %}

{% hint style="success" %}
How do I change the keyfob image? search the js file and swap the image&#x20;

```markup
https://i.ibb.co/DgWRhYj/keyosimg.png
```
{% endhint %}

{% hint style="warning" %}
Do you have backwards compatibility with qb-vehiclekeys?

Yes, but it is recommended to avoid using these events due to the way they are used. Traditional key systems pass a generic string and it wouldnt matter if an entity exsists or not, with mine keys \*must\* be grated after an entity exsists.
{% endhint %}

