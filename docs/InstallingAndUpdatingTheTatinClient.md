[parm]:leanpubExtensions = 1
[parm]:title             = Tatin ReadMe


# Installing and Updating Tatin

## Introduction

Note that you need to worry about this only if you use version 18.0: with version 19.0 or later Tatin will be available in `⎕SE` after a standard installation anyway.

However, installing and updating is, as far as the Tatin client is concerned, _the same thing_, because updating the Tatin client basically means removing the old version and installing the new one.

## How to install the Tatin Client

Instructions:

1. Download the latest release of the Tatin client from <https://github.com/aplteam/Tatin/releases>

2. Unzip it into the `MyUCMDs/` folder.

   The `MyUCMDs/` folder is created by the Dyalog APL installer. Where to find it depends on your operating system:

   * Under Windows it is `(2 ⎕nq # 'GetEnvironment' 'USERPROFILE'),'\Documents\MyUCMDs\'`
   * Otherwise it is `$home/MyUCMDs/`

Any newly started instance of Dyalog 18.0 or later will now come with the Tatin user commands.

As a side effect of executing any of the Tatin user commands the Tatin API will become available via `⎕SE.Tatin`. 

If you want the Tatin API to be available right from the start: this is discussed under "Initializing Tatin".

Putting Tatin into this folder has the benefit that it will be available in all suitable versions of Dyalog APL installed on your machine. It has the drawback that this is a user-specific folder.

Tatin requires version 18.0 Unicode or better, therefore the `]TATIN` user commands won't be listed in either earlier versions of Dyalog or in the Classic version.


## Initialisizing Tatin

As already mentioned, Tatin comes with a self-initializing feature: once installed any suitable version of Dyalog will provide a list of the Tatin user commands once you enter:

```
      ]tatin -?
```

The script `Tatin.dyalog` is the interface between the Dyalog user command framework and the Tatin API: 

* When any of its commands is executed, it will check whether the API is already loaded (`⎕NC '⎕SE.Tatin'`)
* If that's not the case it will...
  1. copy the code into `⎕SE._Tatin`
  2. create a namespace `⎕SE.Tatin` 
  3. establish references in `⎕SE.Tatin` pointing to functions in `⎕SE._Tatin`. 

Now you might want the Tatin API to be around right from the start, so that you can invoke any of the Tatin API functions without first executing any of the Tatin user commands. For example, you might want to have an automated build process available right from the start.

If you are not interested in this, skip the rest of this document.

## On `setup.dyalog`

The way to achieve that goal requires the introduction or modification of a file `setup.dyalog` in your `MyUCMDs\` folder.

A> ### How does `setup.dyalog` work?
A>
A> The magic behind this is that whenever an instance of Dyalog is fired up it checks whether such a script exists. If that is the case it checks whether there is a function `Setup`. 
A>
A> If that is the case it is expected to be a monadic function, and it will be executed automatically as part of the instantiating process of Dyalog APL.
A>
A> This can be used for many things like making changes to the session, specifying function keys or loading stuff into `⎕SE`.

### There is no script `setup.dyalog` yet



### There is already a script `setup.dyalog`