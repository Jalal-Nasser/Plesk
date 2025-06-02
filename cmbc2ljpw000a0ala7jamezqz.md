---
title: "How to Host Your Vercel Project on a Plesk Server"
seoTitle: "Deploy Vercel Project to Plesk Server"
seoDescription: "Learn how to host your Vercel project on a Plesk server, offering control, cost-effectiveness, and server-side customization"
datePublished: Sat May 31 2025 10:09:34 GMT+0000 (Coordinated Universal Time)
cuid: cmbc2ljpw000a0ala7jamezqz
slug: how-to-host-your-vercel-project-on-a-plesk-server
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748686138378/d7e09cfa-9a29-4112-82b6-7917c16c17b9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1748686588952/2e1b5707-d121-494a-990b-c93d3209dada.png
tags: github, vercel, github-actions-1, ssh-keys, plesk, ssh-git, vercel-deployment

---

## Hosting Your Vercel Project on a Plesk Server

While Vercel provides an excellent platform for deploying and hosting web applications, you might need to host your Vercel project on a different server, such as a Plesk server. This could be due to specific requirements, existing infrastructure, or simply for experimentation and learning. This guide will walk you through hosting your Vercel project on a Plesk server.

**Why Host on Plesk?**

Before we dive into the "how," let's briefly consider the "why." Here are a few reasons why you might choose to host your Vercel project on a Plesk server:

* **Control and Customization:** Plesk provides a high degree of control over your server environment. You can customize various aspects of the server, including PHP settings, database configurations, and security measures.
    
* **Existing Infrastructure:** You might already have a Plesk server managing other websites and applications. Consolidating your Vercel project on the same server could simplify management.
    
* **Cost Considerations:** Depending on your usage and the size of your project, hosting on a Plesk server might be more cost-effective in the long run compared to Vercel's pricing structure.
    
* **Learning and Experimentation:** Exploring alternative hosting environments can be a valuable learning experience for developers.
    
* **Specific Requirements:** Some projects might have specific server-side requirements that are better met by a traditional hosting environment like Plesk.
    

**Prerequisites:**

Before you begin, ensure you have the following:

* **A Vercel Project:** You should have a project already deployed and working on Vercel.
    
* **A Plesk Server:** You'll need access to a Plesk server with sufficient resources to host your project. You should also have administrative privileges to manage the server.
    
* **Node.js and npm (or yarn):** Your Plesk server should have Node.js and npm (or yarn) installed. These are necessary for building and running your project.
    
* **Git:** Git is required for cloning your project from your Vercel repository (e.g., GitHub, GitLab, Bitbucket).
    
* **A Domain Name:** You'll need a [domain name pointed](https://jalalnasser.com/how-to-add-a-custom-domain-on-vercel/) to your Plesk server.
    

**Steps to Host Your Vercel Project on Plesk:**

Here's a step-by-step guide to hosting your Vercel project on a Plesk server:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1748685169996/c910c8da-c3ac-4d84-8cb3-e89928dbe323.png align="center")

<iframe width="640" height="360" src="https://www.awesomescreenshot.com/embed?id=40460021&shareKey=218e275e335772838ec4972871c46578"></iframe>

**1\. Obtain Your Project Source Code:**

The first step is to retrieve the source code of your Vercel project. This is typically done by cloning the repository from your chosen Git provider (GitHub, GitLab, Bitbucket).

```bash
git clone <your-repository-url>
cd <your-project-directory>
```

**2\. Build Your Project Locally (Optional but Recommended):**

While not strictly necessary, building your project locally before deploying it to the Plesk server is highly recommended. This helps catch any build errors early on.

```bash
npm install  # or yarn install
npm run build # or yarn build.  Consult your package.json for the correct build script.
```

This will generate a `dist` or `build` directory (depending on your framework), containing the production-ready files for your project.

**3\. Upload Your Project to the Plesk Server:**

There are several ways to upload your project files to your Plesk server:

* **FTP/SFTP:** You can use an FTP or SFTP client (like FileZilla) to connect to your Plesk server and upload the contents of your project's `dist` or `build` direct to the appropriate directory (usually `httpdocs` or a subdirectory within it.
    
* **Plesk File Manager:** Plesk provides a built-in file manager for uploading files directly through the Plesk interface.
    
* **Git Deployment:** If your Plesk server supports Git deployment, you can configure a Git repository within Plesk and push your project code directly to the server. This is often the most efficient and recommended approach.
    

**4\. Configure Your Web Server (Nginx or Apache):**

Plesk typically uses either Nginx or Apache as its web server. You'll need to configure your web server to serve your project files.

* **For Static Sites:** If your Vercel project is a static site (e.g., built with Next.js's static export, Gatsby, or similar), you simply need to configure your web server to serve the files from the `dist` or `build` directory. This usually involves setting the document root to the correct directory.
    
* **For Server-Side Rendering (SSR) or API Routes:** If your Vercel project uses server-side rendering (SSR) or includes API routes, you'll need to set up a Node.js process manager (like PM2) to run your Node.js server. You'll then need to configure your web server to proxy requests to this Node.js server.
    

Here's a general outline of the steps for SSR/API routes:

1\. **Install PM2:** `npm install -g pm2` 2. **Start Your Node.js Server:** `pm2 start <your-server-file.js>` (Replace `<your-server-file.js>` With the entry point to your server application, often found in your `package.json`'s "main" field or a dedicated server file. 3. **Configure Reverse Proxy:** Configure your web server (Nginx or Apache) to proxy requests to your Node.js server. This typically involves setting up a reverse proxy that forwards requests to [`http://localhost:<your-port>`](http://localhost:%3Cyour-port%3E) (replace `<your-port>` With the port your Node.js server is listening on. The exact configuration steps will vary depending on whether you're using Nginx or Apache. Consult Plesk's documentation for details on configuring reverse proxies.

**5\. Configure DNS Records:**

Ensure that your domain name's DNS records are properly configured to point to your Plesk server's IP address. This will allow users to access your project through your domain name. You'll typically need to configure an A record that points your domain name to the server's IP address.

**6\. Test Your Deployment:**

Once you've completed these steps, test your deployment thoroughly. Access your project through your domain name and verify that all functionality is working as expected. Check for any errors in your browser's developer console or in your server logs.

**Example Configuration (Static Site with Nginx in Plesk):**

1. **Upload Files:** Upload the contents of your `dist` or `build` directory to `httpdocs/my-project`.
    
2. **Plesk Nginx Settings:** In Plesk, navigate to the domain's settings and find the Nginx settings. Set the "Document root" to `httpdocs/my-project`.
    
3. **DNS:** Ensure your domain's A record points to your Plesk server's IP address.
    

**Example Configuration (Next.js SSR with PM2 and Nginx):**

1. **Upload Files:** Upload the *entire* project directory (including `node_modules`, `package.json`, etc.) to a directory on your server (e.g., `/var/www/vhosts/`[`yourdomain.com/my-project`](http://yourdomain.com/my-project)). Make sure Node.js has read/write access.
    
2. **Install Dependencies:** SSH into your server and navigate to the project directory: `cd /var/www/vhosts/`[`yourdomain.com/my-project`](http://yourdomain.com/my-project). Then, run `npm install` or `yarn install`.
    
3. **Build (If Necessary):** Run `npm run build` or `yarn build` (if your project requires a build step for production).
    
4. **Start with PM2:** `pm2 start npm --name "my-project" -- start` (This assumes your `package.json` has a "start" script that runs your Next.js server. Adjust the command if necessary.)
    
5. **Configure Nginx Reverse Proxy:** In Plesk, add the following to the "Additional Nginx Directives" section for your domain (adjust port if needed):
    

```nginx
location / {
    proxy_pass http://localhost:3000; # Assuming Next.js server is running on port 3000
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

6. **DNS:** Ensure your domain's A record points to your Plesk server's IP address.
    

**Troubleshooting:**

* **502 Bad Gateway:** This often indicates a problem with the reverse proxy configuration or that your Node.js server is not running correctly. Check your PM2 logs (`pm2 logs my-project`) and your Nginx error logs for clues.
    
* **404 Not Found:** This usually means that your web server is not configured correctly to serve the files from the correct directory. Double-check your document root settings.
    
* **Internal Server Errors:** Check your server logs for detailed error messages. These messages can provide valuable insights into the cause of the problem.
    
* **Permissions Issues:** Ensure that the web server and Node.js processes have the necessary permissions to access the project files.
    

**Conclusion:**

Hosting your Vercel project on a Plesk server can be a viable option if you need more control over your hosting environment, want to consolidate your projects, or have specific server-side requirements. While the process can be more complex than deploying directly to Vercel, it offers greater flexibility and customization. By following the steps outlined in this guide, you can successfully host your Vercel project on a Plesk server and take advantage of the benefits that Plesk provides. Remember to consult Plesk's documentation for detailed instructions on configuring your server and troubleshooting any issues that may arise. Good luck!

### Still can’t solve it

You are free to request my freelance services on [Upwork](https://upwork.com/freelancers/~012b32269d933f4087), [Fiverr](https://pro.fiverr.com/users/jalal), [PeoplePerHour](https://www.peopleperhour.com/freelancer/technology-programming/jalal-nasser-linux-vps-wordpress-seo-php-sql-yjmvjzz), and [Freelancer.com](https://www.freelancer.com/u/jalalnasser)