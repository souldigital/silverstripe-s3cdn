# S3 CDN 

## Configuration

In your local configuration, specify something like

    ---
    Name: locals3settings
    After: 
      - '#s3services'
    ---
	Injector:
	  S3Service:
	    constructor:
	      key: {your_api_key}
	      secret: {your_api_secret}
              region: {region}
	  S3ContentReader:
	    type: prototype
	    properties:
	      s3service: %$S3Service
	      bucket: {your_bucket_name}
              baseUrl: {base_url_for_bucket}
	  S3ContentWriter:
	    type: prototype
	    properties:
	      s3service: %$S3Service
	      bucket: {your_bucket_name}
              baseUrl: {base_url_for_bucket}
      ContentService:
        properties:
          stores:
            File:
              ContentReader: FileContentReader
              ContentWriter: FileContentWriter
            S3Bucket:
              ContentReader: S3ContentReader
              ContentWriter: S3ContentWriter

If you want to use your own filenames (and therefore folders) for assets stored on the S3 Buckets, add the following to your local config
    
    S3ContentWriter:
      use_existing_filenames: true
If you are using your own filenames, just make sure you rewrite them as unique filenames, e.g. append the current timestamp to the name when uploading them. This is to ensure there are no issues with overwriting.