# Serverless-Web-App-AWS
Building a Static Serverless Web Application on AWS.

---

### **Project Overview:**
In this project, you will develop a serverless web application utilizing AWS services such as **Lambda**, **DynamoDB**, and **S3**. The app will enable users to perform **CRUD** (Create, Read, Update, Delete) operations on items stored in a **DynamoDB** table.

### **Project Architecture:**
This project follows the architecture of a **Serverless Web Application** built on AWS.

![image](https://github.com/user-attachments/assets/a45e8b24-22c9-491d-a1a2-0cd600f91306)


### **Steps to Build the Project:**
1. **Set up a DynamoDB table** to store the application data (items).
2. **Create a Lambda function** to manage CRUD operations on the DynamoDB table.
3. **Host static files** (HTML, CSS, and JavaScript) using **S3** to serve the web application's frontend.
4. **Configure CloudFront** to distribute the static content from S3 with low latency, ensuring fast access.

### **Expected Outcome:**
Upon completing this project, you'll have a fully functional **serverless web application** deployed on AWS.  
You will gain practical experience working with AWS services like **Lambda**, **DynamoDB**, **S3**, and **CloudFront** while integrating these services to create a seamless solution.


---

# **Serverless Web Application on AWS: Step-by-Step Guide**

This project walks you through the creation of a **serverless web application on AWS** using services like **S3**, **CloudFront**, **Route 53**, **Lambda**, **DynamoDB**, and **IAM**. The application includes a view counter that increments every time the page is refreshed.

## 🚀 **Step 1: Setup AWS S3 Bucket**

**Purpose:**  
Store HTML, CSS, and JS files for the static web app.

**Process:**
1. Go to the AWS **Management Console**.
2. Create an **S3 bucket** with a unique name (e.g., `serverless-web-app`).
3. Set the **region**, disable **public access**, and enable **SSE-S3 encryption** for security.
4. **Upload Files**: Upload the following to the S3 bucket:
   - `index.html`
   - `style.css`
   - `script.js`

---

## 🌐 **Step 2: Setting Up CloudFront**

**Purpose:**  
Use **CloudFront** as a **Content Delivery Network (CDN)** to ensure low latency and high-speed transfer for the web app stored in S3.

**Process:**
1. Go to the AWS **CloudFront** service.
2. Create a **CloudFront Distribution**:
   - Select your **S3 bucket** as the origin.
   - Choose **Origin Access Control** to secure access to your S3 bucket.
3. **Policy Setup:**
   - Copy the generated CloudFront policy.
   - Paste it in the **S3 bucket policy** under **Permissions** to allow CloudFront access.
4. **Configure Default Root Object:**
   - Set `index.html` as the default root object for CloudFront (the entry point for your web app).

---

## 🌍 **Step 3: Configuring Route 53 and AWS ACM**

**Purpose:**  
Set up **Route 53** for DNS management and **AWS ACM** for enabling a secure, custom domain.

### 1. **Purchasing a Domain:**
   - Use services like **Freenom** (for free domains) or other providers (e.g., **Namecheap**, **GoDaddy**).

### 2. **Creating a Hosted Zone in Route 53:**
   - Go to AWS **Route 53** and create a **Hosted Zone** for your domain (e.g., `shaikabd-cloud.tk`).
   - Choose **Public Hosted Zone** since it’s a web-facing app.

### 3. **Configuring the Domain with Route 53:**
   - Copy the **Name Servers** from Route 53 and paste them into your domain provider’s **DNS settings**.

### 4. **Configuring CloudFront with a Custom Domain:**
   - Go to your **CloudFront distribution** and add the custom domain as alternate domain (e.g., `greeting.shaikabd-cloud.tk`).
   - Use **AWS ACM** to request an **SSL certificate** for your domain.
   - Validate the certificate using **CNAME records** created in Route 53 from CloudFront distribution.

### 5. **Finalizing CloudFront Configuration:**
   - After the certificate is issued, update the CloudFront distribution to use the new **SSL certificate**.
   - Add the **subdomain** (e.g., `greeting.shaikabd-cloud.tk`) and associate it with the CloudFront distribution.

---

## 🔧 **Step 4: Setting Up DynamoDB and IAM for Lambda**

**Purpose:**  
Create a **DynamoDB table** and set up an **IAM role** for the **Lambda function** to enable the view counter functionality.

### 1. **Creating the DynamoDB Table:**
   - In AWS **DynamoDB**, create a table named `serverlesswebapplicationonAWS`.
   - Set the **partition key** to `ID` and add an attribute called `views` (initial value = 1) to track the view count.

### 2. **Enhancing the Web Application:**
   - The web app is enhanced by adding a view counter that increments every time someone visits the page.

### 3. **Creating the IAM Role for Lambda:**
   - Create an **IAM role** that gives the Lambda function permission to interact with DynamoDB.
   - Assign **DynamoDB full access** (for simplicity) and associate the role with AWS Lambda as the trusted entity.

---

## 🖥 **Step 5: Creating and Configuring the Lambda Function**

**Purpose:**  
Create a **Lambda function** to handle the view count updates for the web app.

### 1. **Creating the Lambda Function:**
   - In the **AWS Lambda Console**, create a new function named `serverlessproject`.
   - Select **Python 3.8** as the runtime.
   - Enable **function URL** to simplify integration (avoids API Gateway).
   - Test the function URL to ensure Lambda is running.

### 2. **Troubleshooting Errors:**
   - **Access Denied Error**: Fix missing IAM permissions by attaching the IAM role to the Lambda function.

### 3. **Testing the Lambda Function:**
   - Deploy the updated code and test the Lambda function using the AWS Lambda console or a **curl command**.
   - Verify that the **view count** is successfully incremented upon each refresh of the webpage.

---

## 🔄 **Step 6: Final Testing and Integration**

**Purpose:**  
Integrate the updated JavaScript code with the web app to dynamically display the view counter.

### 1. **Update JavaScript Code:**
   - Create a JavaScript function that fetches the view count from the Lambda URL and updates the counter on the web page.
   - Use **asynchronous functions** and **querySelector** to dynamically update the view count.

### 2. **Update the HTML:**
   - Add a new **counter number** division in `index.html` to display the view count.
   - Ensure the counter uses the correct ID (e.g., `counter-number`).

### 3. **Upload Updated Files to S3:**
   - Upload the updated **`index.html`** and **`script.js`** to the S3 bucket to reflect the changes.

### 4. **Test the Web Application:**
   - Open the website and verify that the view count is updated correctly after each refresh.
   - Monitor the **DynamoDB table** to confirm that the view count is being incremented.

---

🎉 **Project Complete!**  
You have successfully created a **serverless web application** on AWS that dynamically increments a view counter using **Lambda**, **DynamoDB**, and **CloudFront**. 


