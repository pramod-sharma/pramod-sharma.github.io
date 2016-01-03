---
layout: post
comments: true
title:  "Request Response Logging in Faraday"
date:   2015-12-29 05:15:00
categories: Rails, Gems
---
Request and Response Logging in Faraday

<a href='https://rubygems.org/gems/faraday'>Faraday</a> is one of the famous Ruby based HTTP/Rest API Client library. It has over 24 million downloads on RubyGems and is well known among Ruby Community. But while using it I found it quite difficult for me to debug the request and response in Faraday and thats why  I came up with the idea of Faraday based request and response logging gem. You may use this gem directly at 
<a href='https://github.com/pramod-sharma/faraday-request_response_logger'> Faraday Request Response Logger </a>

You may check how I have used Faraday::Response::Middleware for my request response logging inside my middleware. Its been opensource for your convenience and have used env and app variable along with calll method to implement the logger

For the simplicity of post I will concentrate on using gem. Remember I am using it alongwith faraday version 0.9.0, hence you may find issues with your version :-

  * Include Faraday Request Response Logger in your gem file and install it. You need to add it from my github repository as I have not released it on RubyGems
    {% highlight ruby %}
      gem 'faraday-request_response_logger', git: 'https://github.com/pramod-sharma/faraday-request_response_logger'
    {% endhighlight %}
  * Now to use it with Faraday. Use it this way :-
    {% highlight ruby %}
    Faraday.new(url) do |faraday|
  faraday.use Faraday::RequestResponseLogger::Middleware, logger_level: :info, logger: Rails.logger
  faraday.use Faraday::Adapter::NetHttp
end
    {% endhighlight %}


  Use it this way instead of Faraday.new(url)

  Here logger level can be configured to any level as per your requirement and you can configure logger to your custom logger instead of Rails logger. You can use any adapter other than Faraday::Adapter::NetHttp as is mentioned in <a href='https://github.com/lostisland/faraday'> Faraday documentation </a>

  One more configurable option is seperator. It is the intermediatry text between request and response. You can use it as follows :-
    {% highlight ruby %}
      faraday.use Faraday::RequestResponseLogger::Middleware, logger_level: :info, seperator: '**********'
    {% endhighlight %}


Now it will log both your request along with parameters and response alongwith response body, It will log as follows
  {% highlight javascript %}
    Request Log
POST http://api.google.com/v1/random-search-path
"User-Agent: Faraday v0.9.0\n\n{\"search-type\":\"article\",\"query\":{\"search-term\":\"Wifi\"} }"


Response Log
{:status=>200, :headers=>{"content-type"=>"application/json", "date"=>"Sun, 03 Jan 2016 15:14:18 GMT", "server"=>"Apache-Coyote/1.1", "transfer-encoding"=>"chunked", "connection"=>"Close"}, :body=>"[{\"id\":37,\"guid\":\"\",\"name\":\"sad\",\"articleType\":{\"id\":1,\"name\":\"Regular\"}}]"}
  {% endhighlight %}




