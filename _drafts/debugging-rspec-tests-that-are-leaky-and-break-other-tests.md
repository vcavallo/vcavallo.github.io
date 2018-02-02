---
layout: post
title: debugging rspec tests that are leaky and break other tests
---

on cobbler concierge right now some tests seem to leak their db data into other tests
(which is maddening because i'm using database cleaner!!) in order to troubleshoot it
i can't just run the failing tests on their own, because they pass that way... i need
to find a troublesome test and then try a all the other tests in front of it.. i'm
writing a ruby script to do just that.

useful for skipping all remaining tests after a failure - in place of --fail-fast i guess?
```
  before :all do
    $continue = true
  end

  around :each do |example|
    if $continue
      $continue = false
      example.run
      $continue = true unless example.exception
    else
      example.skip
    end
  end
```

useful for checking state (like db) after each test - i once found some leftover data
even though DatabaseCleaner was supposed to be running.
somehow the above issue was related to `around(:each)` usage in tests for some fucky reason
i never figured out.
```
  around(:each) do |ex|
		if codes.any?
			puts "******* there are partner codesssssssssssssssssssssssssssssssssssssssssssssssssss!@!!!!"
			puts "*** codes: { codes }"
			fail
		elsif codes.include?("tx1")
			puts "*********** wtf there is a tx1 fkfkfkfkkfkfkfkkfkfkkfkfkfkf"
			puts "*** codes: { codes }"
			fail
		end
	end
```

