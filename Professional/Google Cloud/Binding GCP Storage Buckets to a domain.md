### Confirming Google Cloud is ready for this process
- In the Google Cloud console, on the project selector page, select or [create a Google Cloud project](https://cloud.google.com/resource-manager/docs/creating-managing-projects)
- Make sure that billing is enabled for your Cloud project. Learn how to [check if billing is enabled on a project](https://cloud.google.com/billing/docs/how-to/verify-billing-enabled)
- Enable the [Compute Engine API](https://console.cloud.google.com/marketplace/product/google/compute.googleapis.com) for your project.
- Have a few website files you want to serve. This tutorial works best if you have at least an index page (`index.html`) and a 404 page (`404.html`)

### Setting up Google Cloud Storage
- Go to [Google Cloud Storage](https://console.cloud.google.com/storage)
- Click **Create bucket**.
- On the **Create a bucket** page, enter your bucket information. To go to the next step, click **Continue**.
	- The bucket name should be `www.<YOURDOMAINHERE>.com`
-  Click **Create**
- In the Google Cloud console, go to the [Cloud Storage Buckets](https://console.cloud.google.com/storage/browser) page.
- In the list of buckets, click the name of the bucket that you created.
- Click the **Upload files** button.
- In the file dialog, browse to the desired file and select it.
	- For our project this should be the `index.html` and `404.html` files.

### Making the files public to the internet
- In the list of buckets, click the name of the bucket that you want to make public
- Select the **Permissions** tab near the top of the page
- Click the **+ Add** button.
- In the **New principals** field, enter `allUsers`
- In the **Select a role** drop down, select the **Cloud Storage** sub-menu, and click the **Storage Object Viewer** option
- Click **Save**
- Click **Allow public access**
	- This will now make those files available to the public internet.
- Go back to the list of buckets
- Click the **Bucket overflow** menu (![](https://cloud.google.com/static/images/overflow_menu_icon.png)) associated with the bucket and select **Edit website configuration**.
- In the website configuration dialog, specify the main page (index.html) and error page (404.html).
- Click **Save**