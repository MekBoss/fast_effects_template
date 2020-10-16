Simple library main goal of which is to reduce performance impact of actors which is used as visual effects, aka nointeractive things.
Note, it does not magically reduce performance impact of actors, (for now) it just cache things.
It mean that first several times it show spaks/smoke/fire/etc. on map loading/transition it would cause some performance drop, but only for the first time.


## HOW TO USE IT?
Copy "thirdparty" folder into you mod folder, copy content of "zscript.zc" and "zmapinfo.txt" files into your mod zscript (optionally delete version number if you already use one) and mapinfo root files respectively and thats it.

Now, inherit all your classes which you want to use as effect only from `generic_fast_effect` class, with next limitations

```
class fire_1 : generic_fast_effect
{
    defaults
    {
        //define things here
        //important note do not redefine NOCLIP and NOINTERACTION flags!!!!!!
    }

    states
    {
        //another important thing, instead of using stop keyword use got in_queue like
        spawn:
            ball a 1;
        goto in_queue;//<-- this would allow actor to be cached
    }
}
```

Then, to show this effect, use ``generic_effect_event.show_effect(effect name, position, velocity)`` (quite a long name, I working on it) to show such effect at specific position and with specific velocity. This function return pointer to actor, so you can also modify it after it was "spawned" through this function.