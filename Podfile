platform :ios, '5.0'

pod 'SDWebImage', :head # We need beyond 3.1 to get a bug fix that prevents an alpha channel from being added to JPEGs (performance hit because it gets treated as a blended layer by CoreAnimation)

# Add Kiwi as an exclusive dependency for the test target
target :UnitTests, :exclusive => true do
   pod 'Kiwi'
end