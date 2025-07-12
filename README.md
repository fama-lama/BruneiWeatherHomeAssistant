# BruneiWeatherHomeAssistant
scrape official Brunei Darussalam Meteorological Department website for latest weather information (Home Assistant)

## Configuration.yaml

```yaml
sensor:

  - platform: rest
    name: "Advisory short - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_advisory_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('header_eng', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour
  
  - platform: rest
    name: "Advisory Weather Conditions - onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_advisory_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: >
        {% if value_json.get('data', {}).get('remarks_eng') %}
            {{ value_json.data.remarks_eng.split('Occasional')[1].split('Wind speed')[0] | trim | truncate(255) }}
        {% else %}
            Unavailable
        {% endif %}
    scan_interval: 3600
    
  - platform: rest
    name: "Advisory start - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_advisory_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('issued_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour        
    
  - platform: rest
    name: "Advisory end - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_advisory_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('ends_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour    
    
    ####
  - platform: rest
    name: "Warning colour - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('colour', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Warning mode - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('stage_eng', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour
    
  - platform: rest
    name: "Warning short - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('header_eng', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour
  
  - platform: rest
    name: "Warning Weather Conditions - onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ (value_json.get('data', {}).get('remarks_eng', 'Unavailable'))[:255] if value_json.get('data', {}).get('remarks_eng') else 'Unavailable' }}"
    scan_interval: 3600
    
  - platform: rest
    name: "Warning start - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('issued_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour       
    
  - platform: rest
    name: "Warning end - Onshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/weather_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('ends_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour        
    
    ####
    
  - platform: rest
    name: "Warning short - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('header_eng', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour
  
  - platform: rest
    name: "Warning Weather Conditions - offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ (value_json.get('data', {}).get('remarks_eng', 'Unavailable'))[:255] if value_json.get('data', {}).get('remarks_eng') else 'Unavailable' }}"
    scan_interval: 3600
    
  - platform: rest
    name: "Warning start - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('issued_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour       
    
  - platform: rest
    name: "Warning end - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('ends_at', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour      
    
  - platform: rest
    name: "Warning colour - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('colour', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour   
    
  - platform: rest
    name: "Warning mode - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_warning_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.get('data', {}).get('warningMode', 'Unavailable') }}"
    scan_interval: 3600  # Update every hour          
    ####
    
  - platform: rest
    name: "Weather - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.weather_forecast_eng if value_json.data.weather_forecast_eng else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Wind - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.wind_eng if value_json.data.wind_eng else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Sea State - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.sea_state_description_eng | replace(', at', '') if value_json.data.sea_state_description_eng else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Sea State Low - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.sea_state_low if value_json.data.sea_state_low else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Sea State High - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.sea_state_high if value_json.data.sea_state_high else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

  - platform: rest
    name: "Remarks - Offshore"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v1/marine_forecast_get"
    method: POST
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    value_template: "{{ value_json.data.remarks if value_json.data.remarks else 'Unavailable' }}"
    scan_interval: 3600  # Update every hour

    ####

  - platform: rest
    name: "Weather - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].weather_desc if value_json.data.observations[0].weather_desc else 'Unavailable' }}"
    scan_interval: 1800
    
  - platform: rest
    name: "Temperature - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].temperature if value_json.data.observations[0].temperature else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 3600

  - platform: rest
    name: "Wind Speed - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].wind if value_json.data.observations[0].wind else 'Unavailable' }}"
    unit_of_measurement: "km/h"
    scan_interval: 3600

  - platform: rest
    name: "Wind Direction - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].wind_direction_eng if value_json.data.observations[0].wind_direction_eng else 'Unavailable' }}"
    scan_interval: 3600

  - platform: rest
    name: "Humidity - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].humidity if value_json.data.observations[0].humidity else 'Unavailable' }}"
    unit_of_measurement: "%"
    scan_interval: 3600

  - platform: rest
    name: "Temperature Feels Like - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].feels_like_c if value_json.data.observations[0].feels_like_c else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 3600

  - platform: rest
    name: "UV Index Live- Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_index if value_json.data.observations[0].uv_index else 'Unavailable' }}"
    unit_of_measurement: "UV Index"
    scan_interval: 3600

  - platform: rest
    name: "UV index 6AM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[3].uv_index if value_json.data.observations[0].uv_data[3].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 8 AM
  - platform: rest
    name: "UV index 8AM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[4].uv_index if value_json.data.observations[0].uv_data[4].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 10 AM
  - platform: rest
    name: "UV index 10AM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[5].uv_index if value_json.data.observations[0].uv_data[5].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 12 PM
  - platform: rest
    name: "UV index 12PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[6].uv_index if value_json.data.observations[0].uv_data[6].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 2 PM
  - platform: rest
    name: "UV index 2PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[7].uv_index if value_json.data.observations[0].uv_data[7].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 4 PM
  - platform: rest
    name: "UV index 4PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[8].uv_index if value_json.data.observations[0].uv_data[8].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 6 PM
  - platform: rest
    name: "UV index 6PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[9].uv_index if value_json.data.observations[0].uv_data[9].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 8 PM
  - platform: rest
    name: "UV index 8PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[10].uv_index if value_json.data.observations[0].uv_data[10].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  # Brunei Airport UV 10 PM
  - platform: rest
    name: "UV index 10PM - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].uv_data[11].uv_index if value_json.data.observations[0].uv_data[11].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800


  - platform: rest
    name: "chance of rain - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].todayrain if value_json.data.observations[0].todayrain else 'Unavailable' }}"
    unit_of_measurement: "%"
    scan_interval: 1800

  - platform: rest
    name: "Sunrise - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].sunrise if value_json.data.observations[0].sunrise else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "Sunset - Brunei Airport"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[0].sunset if value_json.data.observations[0].sunset else 'Unavailable' }}"
    scan_interval: 1800

    ####

  - platform: rest
    name: "Weather - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].weather_desc if value_json.data.observations[5].weather_desc else 'Unavailable' }}"
    scan_interval: 1800
    
  - platform: rest
    name: "Temperature - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].temperature if value_json.data.observations[5].temperature else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "Wind Speed - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].wind if value_json.data.observations[5].wind else 'Unavailable' }}"
    unit_of_measurement: "km/h"
    scan_interval: 1800

  - platform: rest
    name: "Wind Direction - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].wind_direction_eng if value_json.data.observations[5].wind_direction_eng else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "Wind Bearing - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].wind_direction_eng if value_json.data.observations[5].wind_direction_eng is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "Humidity - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].humidity if value_json.data.observations[5].humidity is not none else 'Unavailable' }}"
    unit_of_measurement: "%"
    scan_interval: 1800

  - platform: rest
    name: "chance of rain - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].todayrain if value_json.data.observations[5].todayrain is not none else 'Unavailable' }}"
    unit_of_measurement: "%"
    scan_interval: 1800

  - platform: rest
    name: "Temperature Feels Like - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].feels_like_c if value_json.data.observations[5].feels_like_c is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "UV Index Live - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].uv_index if value_json.data.observations[5].uv_index is not none else 'Unavailable' }}"
    unit_of_measurement: "UV Index"
    scan_interval: 1800

  - platform: rest
    name: "UV index 6AM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[3].uv_index if value_json.data.observations[6].uv_data[3].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 8AM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[4].uv_index if value_json.data.observations[6].uv_data[4].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 10AM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[5].uv_index if value_json.data.observations[6].uv_data[5].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 12PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[6].uv_index if value_json.data.observations[6].uv_data[6].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 2PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[7].uv_index if value_json.data.observations[6].uv_data[7].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 4PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[8].uv_index if value_json.data.observations[6].uv_data[8].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 6PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[9].uv_index if value_json.data.observations[6].uv_data[9].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 8PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[10].uv_index if value_json.data.observations[6].uv_data[10].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "UV index 10PM - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[6].uv_data[11].uv_index if value_json.data.observations[6].uv_data[11].uv_index is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "Sunrise - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].sunrise if value_json.data.observations[5].sunrise is not none else 'Unavailable' }}"
    scan_interval: 1800

  - platform: rest
    name: "Sunset - Kuala Belait"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.observations[5].sunset if value_json.data.observations[5].sunset is not none else 'Unavailable' }}"
    scan_interval: 1800

    ####

  - platform: rest
    name: "Nationwide hourly Temperatures Today (0600hr)"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.hourly.t6am if value_json.data.hourly.t6am is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "Nationwide Hourly Temperatures Today (1000hr)"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.hourly.t10am if value_json.data.hourly.t10am is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "Nationwide Hourly Temperatures Today (1400hr)"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.hourly.t2pm if value_json.data.hourly.t2pm is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "Nationwide Hourly Temperatures Today (1800hr)"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.hourly.t6pm if value_json.data.hourly.t6pm is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800

  - platform: rest
    name: "Nationwide Hourly Temperatures Today (2200hr)"
    resource: "https://bdmd.dotrootbn.com/weatherwx-apiv2/v3/mainpage"
    method: POST
    payload: '{"api_key":"uRDz5W2WnvxE6AX74eMd775Y81Gp8EJ4"}'
    headers:
      Content-Type: "application/x-www-form-urlencoded; charset=UTF-8"
      Origin: "https://www.met.gov.bn"
      Referer: "https://www.met.gov.bn/"
      User-Agent: "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36"
    value_template: "{{ value_json.data.hourly.t10pm if value_json.data.hourly.t10pm is not none else 'Unavailable' }}"
    unit_of_measurement: "°C"
    scan_interval: 1800
 ```
