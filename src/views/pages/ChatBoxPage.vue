<script setup lang="ts">

</script>


<template>
    <header class="my-6">
      <h1 class="text-3xl text-slate-800 mb-4 dark:text-slate-200">Basics & Fundamentals</h1>
      <p class="text-lg text-slate-600 dark:text-slate-400">This guide will give you everything you need to start using the Docs Marketing API to manage audiences, control automation workflows, sync email activity with your database, and more.</p>
    </header>
    <div class="text-slate-600 dark:text-slate-400 space-y-6">

      <!-- Article section -->
      <div class="space-y-6">
        <div class="space-y-4">
          <!-- HTML Bookmark -->
          <!-- The data-scrollspy-target attribute makes the scrollspy work -->
          <h2 id="basics" data-scrollspy-target class="h4 text-slate-800 scroll-mt-24 dark:text-slate-200">The basics</h2>
          <p>
            The Docs Marketing API provides programmatic access to Docs data and functionality, allowing developers to build custom features to do things like sync email activity and campaign analytics with their database, manage audiences and campaigns, and more.
          </p>
          <p>
            To use the Docs API, you need a Docs account. What you can do with the API depends on what level of Docs plan you have. Once you have an account and are logged in, you can get an API key and begin making calls to the API.
          </p>
        </div>
        <div class="space-y-4">
          <h3 class="text-lg font-[650] text-slate-800 dark:text-slate-200">Using Docs</h3>
          <p>
            Whether you're managing your own campaigns, providing Docs services to your customers or clients, or writing a mobile app, the Docs Marketing API has features to manage and sync your contact data.
          </p>
          <p>
            You can also use the Docs API to handle data in different ways for different purposes. If you are syncing a large amount of data with Docs, you can use batches to avoid hitting the API request limits. For building integrations that let other users access data from their own <a class="font-medium text-blue-600 hover:underline" href="#0">Docs accounts</a>, you should <a class="font-medium text-blue-600 hover:underline" href="#0">authenticate with OAuth 2</a>. And if you're developing an app for iOS or Android, the Mobile SDK provides an easy way to work with a mobile-focused subset of the Docs API's functionality.
          </p>
        </div>
      </div>

      <!-- Article section -->
      <div class="space-y-6">
        <div class="space-y-4">
          <!-- HTML Bookmark -->
          <!-- The data-scrollspy-target attribute makes the scrollspy work -->
          <h2 id="api-structure" data-scrollspy-target class="h4 text-slate-800 scroll-mt-24 dark:text-slate-200">API structure</h2>
          <p>
            The Marketing API generally follows REST conventions, with some deviations.
          </p>
          <ul class="list-disc list-inside space-y-2">
            <li>Resources are typically nouns like subscribers or campaigns.</li>
            <li>Subresources can be multiply nested under resources.</li>
            <li>Actions are usually represented by HTTP methods.</li>
            <li>Responses use the generic JSON content type.</li>
          </ul>
          <p>
            We use the API Specification to describe each endpoint. The API self-description also contains type information to help you error-check your requests.
          </p>
          <p>
            The root url for the API is <span class="font-medium text-slate-800 underline dark:text-slate-200">https://&lt;dc&gt;.api.docs.com/3.0/</span>. The &lt;dc&gt; part of the URL corresponds to the data center for your account. For example, if the data center for your account is us6, all API endpoints for your account are available relative to <span class="font-medium text-slate-800 underline dark:text-slate-200">https://us6.api.docs.com/3.0/</span>.
          </p>
          <p>
            There are a few ways to find your data center. It's the first part of the URL you see in the API keys section of your account; if the URL is <span class="font-medium text-slate-800 underline dark:text-slate-200">https://us6.docs.com/account/api/</span>, then the data center subdomain is us6. It's also appended to your API key in the form key-dc; if your API key is <span class="font-medium text-slate-800 underline dark:text-slate-200">0123456789abcdef0123456789abcde-us6</span>, then the data center subdomain is us6. And finally, if you're connecting via OAuth 2, you can find the data center associated with the token via the OAuth Metadata endpoint; for more information, see the OAuth guide.
          </p>
          <div class="text-sm p-4 bg-slate-50 border border-slate-200 rounded-sm dark:bg-slate-800 dark:border-slate-700">
            <div class="flex items-center">
              <svg class="fill-purple-500 shrink-0 mr-4" width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
                <path d="M8 0C3.6 0 0 3.6 0 8s3.6 8 8 8 8-3.6 8-8-3.6-8-8-8Zm0 12c-.6 0-1-.4-1-1s.4-1 1-1 1 .4 1 1-.4 1-1 1Zm1-3H7V4h2v5Z" />
              </svg>
              <p>
                Note: You will see the &lt;dc&gt; placeholder or an actual data center subdomain in examples throughout this documentation. Either way, make sure to replace it in your code with the data center subdomain for your account, or your request may generate an error.
              </p>
            </div>
          </div>
        </div>
      </div>

      <!-- Article section -->
      <div class="space-y-6">
        <div class="space-y-4">
          <!-- HTML Bookmark -->
          <!-- The data-scrollspy-target attribute makes the scrollspy work -->
          <h2 id="connect-api" data-scrollspy-target class="h4 text-slate-800 scroll-mt-24 dark:text-slate-200">Connecting to the API</h2>
          <p>
            You can authenticate requests using either your API key or an OAuth access token, depending on your use case. You should use an API key if you're writing code that tightly couples your application data to your Docs account data; if you ever need to access someone else's Docs account data, you should use OAuth 2.
          </p>
          <p>
            For more information on the Docs OAuth 2 flow, see Access Data on Behalf of Other Users with OAuth 2.
          </p>
          <p>
            If you're integrating with the Docs API using one of the <a class="text-blue-600 font-medium hover:underline" href="#0">official client libraries</a>, you won't need to worry about the implementation details for authentication.
          </p>
        </div>
        <div class="space-y-4">
          <h3 class="text-lg font-[650] text-slate-800 dark:text-slate-200">Authenticate with an API key or OAuth 2 token</h3>
          <p>
            API keys and OAuth 2 tokens can be used to make authenticated requests the same way. We'll refer to both as tokens.
          </p>
          <p>
            You can either use HTTP Basic Authentication or Bearer Authentication.
          </p>
          <p>
            HTTP Basic Authentication:
          </p>
<pre class="overflow-x-auto text-sm text-slate-400 bg-slate-800 border border-slate-700 p-4 rounded-sm">
<code class="font-pt-mono"><span class="text-teal-500">curl</span> --request GET \
      
--url <span class="text-purple-500">'https://&lt;dc&gt;.api.docs.com/3.0/'</span> \
      
--user 'anystring:TOKEN</code>
</pre>
        </div>
      </div>

      <!-- Article section -->
      <div class="space-y-6">
        <div class="space-y-4">
          <!-- HTML Bookmark -->
          <!-- The data-scrollspy-target attribute makes the scrollspy work -->
          <h2 id="api-limits" data-scrollspy-target class="h4 text-slate-800 scroll-mt-24 dark:text-slate-200">API limits</h2>
          <p>
            To improve the experience for all our users, we impose some limits on API requests. These limits prevent a single user from making too many expensive calls at once. Exceeding the limits can result in your API access being disabled, so be cognizant of the quantity and complexity of your requests. Currently there are no options to raise the limit on a per-customer basis.
          </p>
        </div>
        <div class="space-y-4">
          <h3 class="text-lg font-[650] text-slate-800 dark:text-slate-200">Throttling</h3>
          <p>
            The Marketing API has a limit of 10 simultaneous connections. You'll receive a 429 error if you reach the limit. At exceptionally high volumes, you may receive an HTTP 429 or 403 without a JSON body.
          </p>
          <p>
            We recommend that you cache frequently accessed values that do not change often in your application's data store. This will prevent your application from bumping up against the throttling limitations and will likely provide faster access to that data.
          </p>
        </div>
        <div class="space-y-4">
          <h3 class="text-lg font-[650] text-slate-800 dark:text-slate-200">Stream timeouts</h3>
          <p>
            The Marketing API has a 120-second timeout on API calls. You may see this type of timeout after you've made a network socket connection and are already sending and receiving data.
          </p>
          <p>
            Response times are dependent on the complexity of your request and the general load across Docs. Some endpoints in the Marketing API return values that are large and slow to calculate. Once you know what data you need, use the <a class="text-blue-600 font-medium hover:underline" href="#0">pagination and partial response</a> capabilities to request only what is essential to you.
          </p>
          <div class="text-sm p-4 bg-slate-50 border border-slate-200 rounded-sm dark:bg-slate-800 dark:border-slate-700">
            <div class="flex items-center">
              <svg class="fill-teal-500 shrink-0 mr-4" width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
                <path d="M8 0C3.6 0 0 3.6 0 8s3.6 8 8 8 8-3.6 8-8-3.6-8-8-8ZM7 11.4 3.6 8 5 6.6l2 2 4-4L12.4 6 7 11.4Z" />
              </svg>
              <p>
                Note: You will see the &lt;dc&gt; placeholder or an actual data center subdomain in examples throughout this documentation. Either way, make sure to replace it in your code with the data center subdomain for your account, or your request may generate an error.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div> 
</template>