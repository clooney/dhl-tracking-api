DHL Tracking API - PHP
================================
Use PHP to track DHL shipments with DHL Tracking API.

Features
--------
- Real-time DHL tracking.
- Batch DHL tracking.
- Other features to manage your DHL tracking.

Installation
------------

Installation is easy:

    $ composer require trackingmore/trackingmore-sdk-php

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your DHL shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require('vendor/autoload.php');

      use Trackingmore\TrackingMoreException;
      use TrackingMore\Trackings;
        
      $key = 'your api key';
      $response = null;
      $trackings = new Trackings($key);
      
      try {
        $params = ['tracking_number'=>'6832928535','courier_code'=>'dhl'];
        $response = $trackings->createTracking($params);
      } catch (TrackingMoreException $e) {
        echo $e->getMessage();
      }

      print_r($response);

Create trackings (Max. 40 tracking numbers create in one call):

        require('vendor/autoload.php');

        use Trackingmore\TrackingMoreException;
        use TrackingMore\Trackings;
        
        $key = 'your api key';
        $response = null;
        $trackings = new Trackings($key);
        
        try {
            $params = [
                ['tracking_number'=>'1895711370','courier_code'=>'dhl'],
                ['tracking_number'=>'1895711156','courier_code'=>'dhl']
            ];
            $response = $trackings->batchCreateTrackings($params);
        } catch (TrackingMoreException $e) {
            echo $e->getMessage();
        }
        
        print_r($response);


Get status of the shipment:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['courier_code'=>'dhl','created_date_min'=>'2023-08-23T06:00:00+00:00','created_date_max'=>'2023-09-05T07:20:42+00:00'];
        $response = $trackings->getTrackingResults($params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);


Update a tracking by ID:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['customer_name'=>'New name','note'=>'New tests order note'];
        $idString = '99e567a0cbdabf3660b788d850981c81';
        $response = $trackings->updateTrackingByID($idString,$params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);
