DHL Tracking API - Node.js
================================
Use Node.js to track DHL shipments with DHL Tracking API.

Features
--------
- Real-time DHL tracking.
- Batch DHL tracking.
- Other features to manage your DHL tracking.

Installation
------------

Installation is easy:

    gem install trackingmore

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

      require  'trackingmore'

      TrackingMore.api_key = 'your api key'
      
      begin
        params  = {"tracking_number" => "6832928535","courier_code"=>"dhl"}
        response = TrackingMore::Tracking.create_tracking(params)
        puts response
      rescue TrackingMore::TrackingMoreException => e
        puts "Caught Custom Exception: #{e.message}"
      rescue StandardError => e
        puts "Caught Standard Error: #{e.message}"
      end


Create trackings (Max. 40 tracking numbers create in one call):

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = [{"tracking_number" => "1895711156","courier_code"=>"dhl"},{"tracking_number" => "1895711370","courier_code"=>"dhl"}]
      response = TrackingMore::Tracking.batch_create_trackings(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end



Get status of the shipment:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      # Perform queries based on various conditions
      # params  = {"courier_code"=>"dhl"}
      # params  = {"tracking_numbers" => "1895711156,1895711370","courier_code"=>"dhl"}
      params  = {"created_date_min" => "2023-08-23T14:00:00+08:00","created_date_max"=>"2023-08-23T15:04:00+08:00"}
      response = TrackingMore::Tracking.get_tracking_results(params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end


Update a tracking by ID:

    require  'trackingmore'

    TrackingMore.api_key = 'your api key'
    
    begin
      params  = {"customer_name" => "New name","note"=>"New tests order note"}
      id_string = '99e567a0cbdabf3660b788d850981c81'
      response = TrackingMore::Tracking.update_tracking_by_id(id_string, params)
      puts response
    rescue TrackingMore::TrackingMoreException => e
      puts "Caught Custom Exception: #{e.message}"
    rescue StandardError => e
      puts "Caught Standard Error: #{e.message}"
    end