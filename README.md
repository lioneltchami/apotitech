## About
Collect your latest articles from sources such as [dev.to](https://dev.to), and then update the `README.md`.

## Use GitHub Action to update your README

**Step 1:** In your repository, create a file named `README.md.template`.

**Step 2:** Write anything you want within the `README.md.template` file.

**Step 3:** Embed one of the following entities within your `README.md.template`:

- **Article listing:**
```shell
{{ template "article-list" .Articles }}
```
- **Article table:**
```shell
{{ template "article-table" .Articles }}
```

If you are familiar with Go templates, you have access to the `root` variable, which includes the following fields:

- `Articles`: An array of Article. You can view the Article struct definition in [model/article.go](model/article.go).
- `Time`: Updated Time
- `Author`: Author of articles

**Step 4**: Register Github Action
- Create a file `.github/workflows/update-articles.yml` in your repository.
```yml
name: "Cronjob"
on:
schedule:
- cron: '15 0 * * *'

jobs:
    update-articles:
        permissions: write-all
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v3
            - name: Generate README
              uses: huantt/article-listing@v1.1.0
              with:
                username: YOUR_USERNAME_ON_DEV_TO                
                template-file: 'README.md.template'
                out-file: 'README.md'
                limit: 5
            - name: Commit
              run: |
                if git diff --exit-code; then
                    echo "No changes to commit."
                    exit 0
                else
                    git config user.name github-actions
                    git config user.email github-actions@github.com
                    git add .
                    git commit -m "update"
                    git push origin main
                fi
```

**Step 5**: Commit your change, then Github actions will run as your specified cron to update Articles into your README.md file

## Below is my recent articles Lionel Tchami ♾️☁️ collected from dev.to
### Table


<table>
        <tr>
            <td width="300px"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--CksphwCH--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tmcfnb132zrgxgpnfix8.jpg" alt="thumbnail"></td>
            <td>
                <a href="https://dev.to/aws-builders/every-project-deserves-its-cicd-pipeline-no-matter-how-small-19j9">Every Project Deserves its CI/CD pipeline, no matter how small</a>
                <div>TL;DR   In today&#39;s tech industry, setting up a CI/CD pipeline is quite easy. Creating a...</div>
                <div><i>28/08/2023</i></div>
            </td>
        </tr>
        <tr>
            <td width="300px"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--K69CfaQk--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/um9yc5jchgdqn03f59bu.png" alt="thumbnail"></td>
            <td>
                <a href="https://dev.to/softwaresennin/create-your-first-web-app-using-chatgpt-2174">Create your first Web-app using ChatGPT</a>
                <div>Introduction   Language translation is essential in our globalized world, bridging language...</div>
                <div><i>21/08/2023</i></div>
            </td>
        </tr>
        <tr>
            <td width="300px"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--UrbvOo7j--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9lqleb1wzb02sau8m8v1.jpg" alt="thumbnail"></td>
            <td>
                <a href="https://dev.to/aws-builders/localstack-emulate-aws-services-for-local-development-testing-eoj">LocalStack: Emulate AWS Services for Local Development &amp; Testing</a>
                <div>It can be time-consuming, difficult, and even dangerous to create and test cloud-based apps in a...</div>
                <div><i>22/07/2023</i></div>
            </td>
        </tr>
        <tr>
            <td width="300px"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--hzF7BRj4--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xymkz4fh7hvqyl5wcsxl.png" alt="thumbnail"></td>
            <td>
                <a href="https://dev.to/softwaresennin/k8s-quickstart-helm-566o">K8S Quickstart &amp; Helm</a>
                <div>Today, Kubernetes becomes a must for DevOps Engineers, SRE and others for orchestrating containers....</div>
                <div><i>20/08/2023</i></div>
            </td>
        </tr>
        <tr>
            <td width="300px"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--V9FpdGjr--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/iq8fhojv1h7u2m7ad5ia.png" alt="thumbnail"></td>
            <td>
                <a href="https://dev.to/softwaresennin/your-guide-to-prometheus-monitoring-on-kubernetes-with-grafana-gi8">🚀 Your Guide to Prometheus Monitoring on Kubernetes with Grafana</a>
                <div>Introduction:   Hey fam🌟 In the fast-changing tech world of today, keeping an eye on the...</div>
                <div><i>20/08/2023</i></div>
            </td>
        </tr>
</table>


### List

- [Every Project Deserves its CI/CD pipeline, no matter how small](https://dev.to/aws-builders/every-project-deserves-its-cicd-pipeline-no-matter-how-small-19j9) - 28/08/2023
- [Create your first Web-app using ChatGPT](https://dev.to/softwaresennin/create-your-first-web-app-using-chatgpt-2174) - 21/08/2023
- [LocalStack: Emulate AWS Services for Local Development &amp; Testing](https://dev.to/aws-builders/localstack-emulate-aws-services-for-local-development-testing-eoj) - 22/07/2023
- [K8S Quickstart &amp; Helm](https://dev.to/softwaresennin/k8s-quickstart-helm-566o) - 20/08/2023
- [🚀 Your Guide to Prometheus Monitoring on Kubernetes with Grafana](https://dev.to/softwaresennin/your-guide-to-prometheus-monitoring-on-kubernetes-with-grafana-gi8) - 20/08/2023

*Updated at: 2023-09-17T00:28:11Z*