## MBCrashReporter

A simple and basic crash reporter for use in OS X apps:

- The developer provides it with a url to upload to.

- If there's a new crash report on the client's computer, it'll ask the user if he wants to upload it.

###### Example Usage

	#import "MBCrashReporter.h"

	MBCrashReporter* crashReporter = [[MBCrashReporter alloc] initWithUploadURL:@"http://example.com/upload" andDeveloperEmail:@"devemail@example.com"];

	if ([crashReporter hasNewCrashReport] && [MBCrashReporter askToSendCrashReport])
		[crashReporter sendCrashReport];
        
###### Example Server (Ruby with Sinatra)

	post '/upload' do
		unless params[:file] &&
			(tmpfile = params[:file][:tempfile]) &&
			(name = params[:file][:filename]) &&
			name.end_with?(".crash") &&
			tmpfile.size <= 1024*100
			
			halt(400)
		end
	
		File.open("crashes/"+name, "w") do |f|
			f.write(tmpfile.read)
		end
		
		"Uploaded."
	end
	
###### LICENSE

This program is licensed under GNU GPL v3.0 (see LICENSE)

Attributes are appreciated.