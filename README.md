# XList
Extended list for ObjectScript with support for declarative and functional programming

## Introduction
Besides extended methods to instatiate lists, insert and remove items the XList provides support for functional programming.
Key to this feature is wrapping methods as objects itself to be able to pass them to other methods. Therefore with the XList comes a bunch of classes to express methods as objects.
For example if you want to use methods or properties of the items contained in your list you would use the InstanceMethod- and InstanceProperty-classes. If you want all items in the list being passed to any classmethod just create a corresponding ClassMethodAction/ClassMethodConverter and pass it to the dedicated function of the XList.

Functional programming has a massive impact on understanding what a piece of code tries to achieve because it is more human readable compared to a couple of lines iterating through list items and and checking and setting some values.

## Examples
Imagine you have a list of objects and then think about the amount of code you have to write to get the biggest value for the property "Height" of all items in the list.
In the extended list you can program it functionally as a one-liner and it looks like this:
```
set biggestHeight = xListOfObjects.max(##class(%ZLib.delegates.InstancePropertyConverter).create("Height"))
```
In the same manor you can get the item having the biggest value:
```
set biggestHeightItem = xListOfObjects.maxItem(##class(%ZLib.delegates.InstancePropertyConverter).create("Height"))
```

Getting a sublist with all items that have their property "Description" empty:
```
set subXList = xList.select(##class(%ZLib.delegates.InstancePropertyEqualsConverter).create("Description",""))
```

How about summing up the item's prices (Property "Price"):
```
set sum = xList.sum(##class(%ZLib.delegates.InstancePropertyConverter).create("Price"))
```

Also the XList provides functions to deal with usual lists.
Let's say you have a ususal %ListOfDataTypes containing Ids (primary keys) and you want to gather all the corresponding objects:
```
set xListOfObjects = ##class(%ZLib.XListOfDataTypes).listConvertAll(usualList, ##class(%ZLib.delegates.ClassMethodConverter).create("myPackage.MyClassName", "%OpenId", 0))
```

Or just pass all items to your coolServiceMethod which expects a listItem as parameter:
```
do xListOfObjects.foreach(##class(%ZLib.delegates.ObjectMethodAction).create(myCoolServiceInstance, "myCoolMethod"))
```

## Installation
Just import the classes to your caché/iris in your favourite way. It will be located in %SYS package %ZLib so that you can use it from any namespace.

## Additional
Of course you can use the method and property wrapper classes of this project not only with the XList but in any case you could think of in which passing a method or a property-getter to another method would be helpful.

## Docker
 
### Prerequisites
Make sure you have [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) and [Docker desktop](https://www.docker.com/products/docker-desktop) installed.
### Installation
Clone/git pull the repo into any local directory
```
$ git clone https://github.com/rcemper/PR_objectscript_extendedlist.git
```
```
$ docker compose up -d && docker compose logs -f
```
To open IRIS Terminal do:
```
$ docker-compose exec iris iris session iris
USER>
```
or using **WebTerminal**
```
http://localhost:42773/terminal/
```
To access IRIS System Management Portal
```
http://localhost:42773/csp/sys/UtilHome.csp
``` 