## Purpose: Remind myself the differences on Deployment between GitHub Pages, Vercel, and Netlify
\
\
&nbsp;

| GitHub | Vercel (manual) | Netlify (manual) |
| --- | --- | --- |
| static | staic & serverless | static & serverless | 
| INSTALL in project: | INSTALL globally: 
| `npm i gh-pages` | `sudo npm i -g vercel` | `sudo npm i netlify-cli -g` |
| ADD properties to Package.json: | N/A | N/A |
| `"homepage": "http://geeeedev.github.io/shopping-list-app"`, | | |
| `"scripts": {`
| `    "predeploy":"npm run build",`
| `    "deploy":"gh-pages -d build"`
| `    "start": "react-scripts start",`
| `    "build": "react-scripts build", ...} `| 
| PREDEPLOY: |
| initialize and upload project to GitHub as usual:<br/> Git init, git add ., git commit -m “…” on project <br/>Create Github repo and git remote add origin to it| N/A | `npm run build`  in project terminal <br> to generate a production build copy |
| DEPLOY: | | |
| `npm rum deploy` | `vercel`  | `netlify deploy` <br/>(remember to `npm run build` first)|
| predeploy (npm run build) will be auto-initiated before deploy (gh-pages -d build)<br>a branch named gh-pages which hosts the deployed app will be created on GitHub<br>homepage property holds the URL for live preview | to activate Vercel CLI and <br> initiate Vercel deployment | deploys a Netlify draft/test version from local directory |
| N/A | Set up and deploy “…current project path…”? Y | What would you like? Create & config a new site |
|     | Which Scope? geeeedev | - Team? geeeedev’s Team |
|     | Link to existing? N | |
|     | Proj name? … | Site name? … |
|     | Directory for code? ./ | Publish directory? ./build |
|     | Build Command? npm run build (Default)| |
|     | Output Dir? build (Default) | |
|     | Dev Command? React-script start (Default) | |
|     | Override settings? N| |
|     | Draft site provided (Inspect link)<br>Prod site generated | Draft site generated |
|     | | `netlify deploy --prod` <br> deploy a prod site |
|     | Production site generated automatically | Production site generated<br>(only after `netlify deploy --prod`) |
|     | click `Connect a Git Repository`<br> to connect to a Git repo for CI/CD | click `Link site to Git`<br> to connect to a Git repo<br>(under Deploys - Deploy Settings - Build & Deploy - CD) |
|     | [Vercel ???]() | [Netlify Deployment Explained](https://levelup.gitconnected.com/how-to-deploy-a-react-app-with-netlify-set-up-continuous-deployment-via-github-53859dcdaf40) |
|     | tag `/_src` to view Vercel source code<br>https://geeeedev.vercel.app/_src | |
| CHECK: | | |
| access GitHub Settings > GitHub Pages > see "published" msg | | |
| RE-DEPLOY:  | | |
| commit and push to GitHub as usual<br>code push to master branch as usual | | |
| run `npm run deploy` again |  | `npm run build`<br> to RE-build a production copy |
| (will repeat build and deploy process with your new code)<br>(this is separate from commit/push to master - must do both manually to stay synced)<br>`npm run deploy` processes a build copy and post it to the gh-pages branch<br> which is separate from master branch. Live site is spinned off of gh-pages branch. | `vercel`<br> re-deploy to draft site | run again `netlify deploy`<br> re-deploy a draft version from local directory |
|  | `vercel --prod`<br> manually REDEPLOY to prod site<br> sync draft site to prod site | or run `netlify deploy --prod`<br> bypass draft and build prod version directly |
|  | | |

\
\
&nbsp;
(combine below notes with table below)
### Deploy with Vercel (using GitHub private repo - Continuous Integration/Deployment)
With Continuous Integration/Continuous Deployment:
- Upload code to a Git repo (like GitHub) and deployment will automatically triggered
Upload all code on GitHub repo (private or not)
In Vercel, hook up and specify GitHub repo with Vercel project and deploy from there.
Since project is hooked up to GitHub repo, Continuous Integration/Deployment will happen when code changes are pushed to GitHub repo
\
&nbsp;

| Vercel (CI/CD) | Netlify (CI/CD) |
| --- | --- |
| Try Next with GitHub (CI/CD) | |
| CI/CD Deployment thru Git Repo: | (no need to manually run RE-deploy commands) |
| (document steps for Vercel) | (document/confirm steps for Netlify)|
| (document steps for Vercel) | `npm run build`<br> run a production build copy |
| (document steps for Vercel) | push to Git repo again to include the build folder |
| (document steps for Vercel) | click `New Site from Git` in Netlify |
| (document steps for Vercel) | import build from GitHub repo |
| (document steps for Vercel) |  |
| (document steps for Vercel) |  |
| (document steps for Vercel) |  |
| (document steps for Vercel) | Access App Dashboard  |
| (document steps for Vercel) | click Site Settings ?? |
| (document steps for Vercel) | click Build & Deploy, Continuous Deployment |
| (document steps for Vercel) | Branch to deploy: master (?) |
| (document steps for Vercel) | Build Command: `CI= npm run build` |
| (document steps for Vercel) | Publish directory: build |
| (document steps for Vercel) | Show Advanced: |
| (document steps for Vercel) | ENV variable: API Keys, secrets |
| (document steps for Vercel) | click Deploy Site |
| (document steps for Vercel) |  |
| (document steps for Vercel) |  |
| (document steps for Vercel) |  |
| (document steps for Vercel) | adjust Build Command in Netlify CI/CD only: |
| (document steps for Vercel) | `CI= npm run build`<br>(under Deploys - Deploy Settings - Build & Deploy - CD - Build Command) |
| (document steps for Vercel) | add ENV variables for API or secret keys<br> (under Deploys - Deploy Settings - Advance build setting) |
| (document steps for Vercel) | ??? `netlify deploy` - deploy a draft version |
| (document steps for Vercel) | draft site provided |
| (document steps for Vercel) | click `Trigger Deploy` button in Netlify to deploy to prod site |
| (document steps for Vercel) | `netlify deploy --prod` to deploy to production site