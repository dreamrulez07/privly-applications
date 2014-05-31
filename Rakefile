require 'rubygems'
require 'bundler/setup'

require 'selenium-webdriver'

desc 'Run Jasmine tests with Webdriver'
task :webdriver do

  # Detect which browser we want to run
  case ENV['browser']
  when 'chromium'
    # TODO: detect chromium path? I use Linux, this is the path on my machine
    Selenium::WebDriver::Chrome.path = '/usr/lib/chromium-browser/chromium-browser'
    driver = Selenium::WebDriver.for :chrome
  when 'firefox'
    driver = Selenium::WebDriver.for :firefox
  else
    raise ArgumentError, 'Unknown browser requested'
  end

  # Finally, we load the spec runner HTML page with WebDriver
  driver.navigate.to 'http://localhost:3000/apps/Help/new.html'
  status = driver.execute_script('return consoleReporter.status;')
  output = driver.execute_script('return consoleReporter.getLogsAsString();')
  driver.quit

  print output

  # Make sure to exit with code > 0 if there is a test failure
  raise RuntimeError, 'Failure' unless status === 'success'

end
