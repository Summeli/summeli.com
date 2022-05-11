---
id: 1900
title: 'Using the proximity sensor as a button'
date: '2010-09-25T12:32:24+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=1900'
permalink: /1900/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Symbian Development'
---

The Proximity sensor is usually used to detect when the phone is near of the user’s ear, so the display can be turned off when speaking into the phone. The Symbian OS has an API for the proximity sensor, so it can also be used as a button.  
My experience from the proximity sensor suggest that you shouldn’t use it when you are needing a high resolution refresh rates for the button( action games), since the API gives updates only few times in a second.

<div class="wp-caption aligncenter" id="attachment_1953" style="width: 360px">[![](http://www.summeli.com/wp-content/uploads/2010/09/5230.jpg "prox_sensor")](http://www.summeli.com/wp-content/uploads/2010/09/5230.jpg)The Proximity sensor is located near the ear piece on the phone

</div>**Using the API**

The Proximity sensor can be used via sensor framework. See this forum.nokia example[ http://wiki.forum.nokia.com/index.php/S60\_Sensor\_Framework](http://wiki.forum.nokia.com/index.php/S60_Sensor_Framework) )

Initializing the proximity sensor can be done with following snippet

```
<pre class="brush: cpp; title: ; notranslate" title="">
    CSensrvChannelFinder* SensrvChannelFinder = CSensrvChannelFinder::NewLC();
    RSensrvChannelInfoList ChannelInfoList;
    CleanupClosePushL( ChannelInfoList );
    TSensrvChannelInfo mySearchConditions; // none, so matches all.
    mySearchConditions.iChannelDataTypeId = KSensrvChannelTypeIdProximityMonitor;
    SensrvChannelFinder->FindChannelsL(ChannelInfoList,mySearchConditions);
     // do something with the ChannelInfoList
    iSensrvChannel = CSensrvChannel::NewL( ChannelInfoList[0] );
    iSensrvChannel->OpenChannelL();
    ChannelInfoList.Close();
    CleanupStack::Pop( &ChannelInfoList );
    CleanupStack::PopAndDestroy( SensrvChannelFinder );
```

After the proximity sensor channel has been opened into iSensrvChannel it can be read with timer and calling

```
<pre class="brush: cpp; title: ; notranslate" title="">
iSensrvChannel->StartDataListeningL( this, 1,1,0);
```

After this the data is being received trough MSensrvDataListener interface class via DataReceived function:

```
<pre class="brush: cpp; title: ; notranslate" title="">
void ProximityButton::DataReceived( CSensrvChannel& aChannel, TInt aCount, TInt aDataLost )
	{
    if ( aChannel.GetChannelInfo().iChannelType ==  KSensrvChannelTypeIdProximityMonitor )
    	{
    	TSensrvProximityData data;
    	for( TInt i = 0; i < aCount; i++ )
    		{
    		TPckgBuf<TSensrvProximityData> dataBuf;
    		aChannel.GetData( dataBuf );
    		data = dataBuf();
    		TSensrvProximityData::TProximityState state = data.iProximityState;
    		if ( iLastState != state )
    			{
    			if( state == TSensrvProximityData::EProximityIndiscernible )
    				{
    				//button up
    				PostKeyEvent( EFalse );
				}
    			if( state == TSensrvProximityData::EProximityDiscernible )
    				{
    				//button down
    				PostKeyEvent( ETrue );
    				}
    			}
    		iLastState = state;
    		}
    	}
    dataRequested = EFalse;
	}
```

After this you just have to implement the PostKeyEvent function where you can emit a key event.  
The proximity sensor can also be used through [Qt Mobility API’s sensor API](http://doc.qt.nokia.com/qtmobility-1.0/sensors-api.html) but this time I wasn’t using it.