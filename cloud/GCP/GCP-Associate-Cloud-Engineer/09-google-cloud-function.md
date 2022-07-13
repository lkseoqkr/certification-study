# Cloud Functions
- execute some code when an event happens?
  - A file is uploaded in Cloud Storage
  - An error log is written to Cloud Logging 
  - A message arrives to Cloud Pub/Sub
- Run code in response to events
- Pay only for what you use
  - Number of invocations
  - Compute Time of the invocations
  - Amount of memory and CPU provisioned
- Each execution runs in a separate instance
- Time Bound - Default 1 min and MAX 9 minutes(540 seconds)
# Cloud Functions - Concepts
- Event : Upload object to cloud storage
- Trigger: Respond to event with a Function call
- Events are triggered from 
  - Cloud Storage 
  - Cloud Pub/Sub 
  - HTTP POST/GET/DELETE/PUT/OPTIONS Firebase 
  - Cloud Firestore 
  - Stack driver logging
# Example Cloud Function
- HTTP - Node.js
```
exports.helloHttp = (req, res) => {
  res.send(`Hello ${escapeHtml(req.query.name || req.body.name || 'World')}!`);
};
```
- Pub/Sub - Node.js
```
exports.helloPubSub = (message, context) => {
  const name = message.data
    ? Buffer.from(message.data, 'base64').toString()
    : 'World';
  console.log(`Hello, ${name}!`);
};  
```
# Cloud Functions - **Remember**
- No Server Management
- Cloud Functions automatically spin up and back down in response to events
- Cloud Functions are recommended for responding to events
  - Cloud Functions are **NOT ideal for long running processes**
    - Time Bound - Default 1 min and MAX 9 minutes(540 seconds)
# Cloud Run & Cloud Run for Anthos
- Cloud Run - "Container to Production in Seconds"
  - Built on top of an open standard - Knative
  - Fully managed serverless platform for containerized applications
- Fully integrated end-to-end developer experience
  - No limitations in languages, binaries and dependencies
- Anthos - Run Kubernetes clusters anywhere
  - Cloud, Multi Cloud and On-Premise
- Cloud Run for Anthos
  - Deploy your workloads to Anthos clusters running on-premises or on Google Cloud
