CocoaPodsError
==============

Project showing error on CocoaPods -- just pod install to see.

Steps to Repro:

1) Create a new project
2) Add a podfile that gets the head of a repo. I used `pod 'SDWebImage', :head`
3) pod install
4) Add a new pod to the podfile (I had the same error whether or adding Kiwi or TTTAttributedLabel).
5) pod install

// Same error on Ruby 2.0.0

### Stack

```
   CocoaPods : 0.17.0.rc7
        Ruby : ruby 1.9.3p327 (2012-11-10 revision 37606) [x86_64-darwin12.3.0]
    RubyGems : 1.8.25
        Host : Mac OS X 10.8.3 (12D78)
       Xcode : 4.6.1 (4H512)
Ruby lib dir : /Users/Max/.rvm/rubies/ruby-1.9.3-p327/lib
Repositories : master - https://github.com/CocoaPods/Specs.git @ 037c983885bcc42e0bd5af8c9e900b4d965b2cab
```

### Podfile

```ruby
platform :ios, '5.0'

pod 'SDWebImage', :head # We need beyond 3.1 to get a bug fix that prevents an alpha channel from being added to JPEGs (performance hit because it gets treated as a blended layer by CoreAnimation)

# Add Kiwi as an exclusive dependency for the test target
target :UnitTests, :exclusive => true do
   pod 'Kiwi'
end
```

### Error

```
ArgumentError - Illformed requirement ["= HEAD based on 3.2"]
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:83:in `parse'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:108:in `block in initialize'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:108:in `map!'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:108:in `initialize'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:46:in `new'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/requirement.rb:46:in `create'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/dependency.rb:52:in `initialize'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/dependency.rb:77:in `initialize'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/dependency.rb:214:in `new'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/vendor/dependency.rb:214:in `merge'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/dependency.rb:180:in `merge'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:76:in `block in dependency'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:75:in `each'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:75:in `inject'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:75:in `dependency'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:106:in `block in required_version'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:106:in `each'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:106:in `find'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:106:in `required_version'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-core-0.17.0.rc7/lib/cocoapods-core/specification/set.rb:88:in `specification'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:157:in `block (2 levels) in find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/user_interface.rb:113:in `message'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:152:in `block in find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:148:in `each'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:148:in `find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:164:in `block (2 levels) in find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/user_interface.rb:113:in `message'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:152:in `block in find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:148:in `each'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:148:in `find_dependency_specs'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:65:in `block (2 levels) in resolve'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/user_interface.rb:52:in `section'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:63:in `block in resolve'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:62:in `each'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/resolver.rb:62:in `resolve'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer/analyzer.rb:286:in `block in resolve_dependencies'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/user_interface.rb:52:in `section'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer/analyzer.rb:284:in `resolve_dependencies'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer/analyzer.rb:56:in `analyze'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer.rb:157:in `analyze'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer.rb:92:in `block in resolve_dependencies'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/user_interface.rb:52:in `section'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer.rb:91:in `resolve_dependencies'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/installer.rb:84:in `install!'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/command/project.rb:40:in `run_install_with_update'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/command/project.rb:70:in `run'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/claide-0.2.0/lib/claide.rb:535:in `run'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/lib/cocoapods/command.rb:36:in `run'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/gems/cocoapods-0.17.0.rc7/bin/pod:16:in `<top (required)>'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/bin/pod:19:in `load'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/bin/pod:19:in `<main>'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/bin/ruby_noexec_wrapper:14:in `eval'
/Users/Max/.rvm/gems/ruby-1.9.3-p327@rails3tutorial2ndEd/bin/ruby_noexec_wrapper:14:in `<main>'
```

