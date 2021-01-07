# Gatsby.js blog pulling data from Notion.so via Python
This is a separately maintained repository based on the works of @ArnaudValensi and @tfaieta

See the original readme below.

## Improvements from the original code
- Renamed variables to follow Python `snake_case` convention
- Enabled support for Unicode languages (tested with Vietnamese)
- Added `virtualenv` for easy development with PyCharm
- Removed `pipenv` support because Github Actions itself already runs in a virtual environment, so it's not needed; and with `pipenv`, I experienced errors related to image processing. Therefore, the deployment workflow uses pure `python` command.

## Steps to setup local dev environment
1. Install Node.js >= 14.15.3
2. Install Python 3.8 and add its directories to `PATH`
- Critical note: this does not work with version 3.7 and earlier due to dependency conflicts

3. Install `git` (if you are on Windows, choose to use Unix-tools such as find, sort, mv for easy access to Linux commands)
4. Install PyCharm for easy management of virtual environments (optional)
5. Open any Terminal (or Command Prompt) window you have, clone this repo using command:
- `git clone https://github.com/huydhoang/huydhoang.com.git`
- `Enter` to execute
- `mv huydhoang.com {YOUR-PREFFERED-PROJECT-NAME}` to change the folder's name to your liking

6. Open the cloned folder PyCharm, click on `Terminal` window tab at the bottom panel, remember to hit `Enter` after every command
- Alternatively, if you don't prefer PyCharm, `cd {YOUR-PREFFERED-PROJECT-NAME}` to get into the cloned folder

7. Start your own git repo for version control:
- `rm -rf .git` to remove my git hidden folder
- `git init` to initialize yours

8. Install Yarn and Gatsby.js
- `npm i -g yarn`
- `yarn global bin` to display Yarn's directory for binaries and add it to `PATH` environment variable
- `yarn` to start rebuilding the `node-modules` folder
- `yarn add global gatsby-cli` (or `npm i -g gatsby-cli` if you don't use Yarn. I personally like Yarn because of its speed and CLI interface.)

9. Steps to import Notion posts
- Create a file named`.env` to hold your Notion.so secrets (see `.env.example`)
- Input your `NOTION_TOKEN` and `NOTION_ROOT_PAGE_ID`
- Refer to the original readme below if you don't know how to get those ids 
- Audit the Python script -- can be located in `./bin/get-blog-posts.py`
- After that, `yarn import-notion-posts` to start importing your notes from Notion

10. `gatsby develop` to start development server
- Your site will be live at `http://localhost:8000` by default

---
## Original readme by Arnaud Valensi [arnaudvalensi.github.io](https://arnaudvalensi.github.io/)

My personal blog. Powered by [GatsbyJS](https://www.gatsbyjs.com/) and [Notion](https://www.notion.so/)

This blog uses content from notes made in [notion.so](https://www.notion.so/) and automatically deploys on github pages.

You can read my blog post about this, [here](https://arnaudvalensi.github.io/blog/making-a-blog-using-notion-gatsby-and-github-pages/)

## To run locally

Copy the file `.env.example` to `.env` and fill the `NOTION_TOKEN` and `NOTION_ROOT_PAGE_ID` variable.

Follow [this](https://www.redgregory.com/notion/2020/6/15/9zuzav95gwzwewdu1dspweqbv481s5) to see how to get your notion token.

The `NOTION_ROOT_PAGE_ID` is the ID of the root note of your blog. The root note is a regular notion note which indexes all the posts you want to import in the blog, therefore, it should only list links to other notes.

If the link of your root note is this `https://www.notion.so/Blog-83f4047341534d6bb846b1f561a13173`, the id is this: `83f4047341534d6bb846b1f561a13173`

Then you can do `yarn import-notion-posts` to import post from notion to `./content/blog`.

Finally, you can do `yarn develop` to run the blog locally.

## To manually deploy to github pages

`yarn import-notion-posts` to import the posts from notion.

`yarn deploy` to build and publish the `public` directory to github page.

To deploy on github pages, you have to use your username as repository name. See [here](https://pages.github.com/) for more information.

If you don't want to deploy to github pages, you can host the content of the `public` directory anywhere you want.

## Automatically deploy to github pages

If you push this repository to github, it will use the [github action](https://github.com/features/actions) stored in `.github/workflows/deploy.yml` and automatically import your post from notion and build the blog.

You have to let github know your `NOTION_TOKEN` and `NOTION_ROOT_PAGE_ID`. To do so, fill the info as [github secret](https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets).

The github action is configured to import the blog posts and rebuild the blog either:

- every day at midnight UTC
- each time you push on master
- if you manually trigger the action on github

## Posts

To make the system work, you have to fill the following elements on your blog posts:
![exampel](https://user-images.githubusercontent.com/604486/95316471-24c4ee80-0894-11eb-8399-f99701b801da.png)

