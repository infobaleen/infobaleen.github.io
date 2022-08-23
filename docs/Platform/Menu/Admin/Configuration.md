# Configuration

In the configuration page you can add connections to data, for example databases, and you can also add connections to integrations that you want to export data to, for example an email service.

## Databases

A database configuration is set up to fetch data into the platform, and it can be a connection to something like a data lake or a mysql server. It can look something like in the image below. Note that a parameter like `${db-user}` needs to be added in the `Secrets` page.

<img width="976" alt="Screenshot 2022-07-01 at 11 28 48" src="https://user-images.githubusercontent.com/4352260/176867875-be6a64af-1a67-48d9-88f5-689d763718d7.png">

## Integrations

An integration configuration is set up to export data from the platform.  It can look something like the facebook-export in the image below (emails are exported to Facebook). Note that a parameter like `${fb-token}` needs to be added in the `Secrets` page.

<img width="837" alt="Screenshot 2022-07-01 at 11 34 13" src="https://user-images.githubusercontent.com/4352260/176868658-b99b6f52-8a53-48f6-8e9e-b42275d10329.png">




