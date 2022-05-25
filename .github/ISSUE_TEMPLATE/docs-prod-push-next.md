---
name: Docs prod push NEXT
about: prod push template
title: Doc prod push NEXT
labels: prod-push
assignees: ''

---



## Using this Epic for Prod Push Issues

This ZenHub Epic contains the review checklist you need to do to push the [Code Engine](https://cloud.ibm.com/docs/codeengine) doc content to prod. Issues that are to be built in this prod push should be attached to this Epic.

## Prod Push Review
As you go through the following list, mark off each item as you complete it.

### Before you push

**Remember**: Avoid prod pushes at the end of the day, if possible. You might need to make changes if something goes wrong!

- [ ] In the #doctopus-coligo](https://ibm-argonauts.slack.com/messages/CSYM4GUQ2) channel, check with the other writers and make sure that you're all clear to do a prod push.
a. Other writers should not remove staging tags until the push is out.
b. Other writers should wait until you give them the OK to resolve their new work items and remove staging tags for new changes.

- [ ] Move this work item into the `In Progress` pipeline, make sure that the **prod-push** label is added to the issue, and assign it to you.

- [ ] Confirm that each issue linked to this epic has been resolved. Also confirm that each completed issue was properly linked to this epic (check the `Review Complete` pipeline for issues that may not have been labelled under this epic, and ask the owners).

- [ ] Update the `landing.json` page with the latest changes. Keep only three changes on page. Do not put links in descriptions. _(Not applicable yet)_

- [ ] Review the issue or prod PRs for new content or updates that are valuable to include in the [Release Notes](https://github.ibm.com/coligo/docs/blob/master/release-notes.md) page. Don't include things like grammar, links, light restructuring, troubleshooting, or overly negative things.

- [ ] Taking no more than 10 minutes to complete, review some content in the staging [Code Engine Docs](https://test.cloud.ibm.com/docs/codeengine?topic=codeengine-getting-started) docs.
a. Does text display correctly: lists, paragraphs, headings, code, tables, etc.?
b. Does the product name show correctly in the landing page?
c. Do images display?
d. Click links in the immediate navigation of the changed topics (parent and children). Do they work?
e. Click at least 3 inline links. Do they work?
f. Search the doc for common search queries. Is the changed content showing up in search results? Do the search results take you to the expected content?

- [ ] Run a [prod link checker build on the hosted Jenkins](https://wcp-doctopus-docs-jenkins.swg-devops.com/job/link-checker-v2/) for Code Engine docs and fix any broken links.

### Push the changes

- [ ] Open the prod pull request for **both the product docs and CLI docs**:
      * Code Engine docs: https://github.ibm.com/cloud-docs/codeengine/pulls
      * CLI docs: https://github.ibm.com/cloud-docs/codeengine-cli/pulls

- [ ] Review the changes one last time to verify that the PR contains the correct changes.

- [ ] Complete the Github review requirement.

- [ ] Merge the changes in **both product and CLI docs**, then delete the prod push branch.

- [ ] Stick around to confirm that the prod push worked OK or arrange for someone else to be there when the build is finished (about an hour).

### After the push is done

- [ ] In the summary of this issue, change `<next>` to the date the build was run.

- [ ] In this same repo, open a new issue by using the **Prod Push** template. Set the **Pipeline** to `Backlog`, then click **Create an epic**. On the following page, don't worry about attaching items to the epic, just click **Create Epic**.

- [ ] Make sure that the next prod push epic issue is actually a ZenHub Epic (a lot of times it just gets created as a regular GitHub issue). If it's not an Epic, in the issue, on the right hand menu, when you click the `Epics` category, there is an option to convert it to an epic.

- [ ] Let writers know that the build has been pushed to production.  

### After the changes are live

- [ ] Taking no more than 10 minutes to complete, review some content in the production Cloud docs.
a. Does text display correctly: lists, paragraphs, headings, code, tables, etc.?
b. Does the product name show correctly in the landing page?
c. Do images display?
d. Click links in the immediate navigation of the changed topics (parent and children). Do they work?
e. Click at least 3 inline links. Do they work?
f. Using search for common search queries, is the changed content showing up in search results? Do the search results take you to the expected content?
g. Look for draft comments or other "comments to developers."
h. Ask the writer what content shouldn't be showing and search for it.
i. If translations were built, check at least one translation topic and one translation image for all languages. **Note**: To load translations, add `?locale=<lang_abbreviation>` to the URL. If you find an issue during testing, contact Bryan, our translation coordinator in China.

- [ ] For any topics that have been moved or removed, verify that redirects are working.

- [ ] In the Github issue, confirm that you've checked the changes.

- [ ] Let the writers know that the build is done and they can verify their content in production.

- [ ] If there were any PRs from the [Staging ](https://github.ibm.com/cloud-docs/codeengine/pulls)/ [Prod ](https://github.com/ibm-cloud-docs/codeengine/pulls)repos, let them know that the fix is in prod and close out those PRs. Same for CLI repos: [Staging ](https://github.ibm.com/cloud-docs/codeengine-cli/pulls)/ [Prod ](https://github.com/ibm-cloud-docs/codeengine-cli/pulls)repos.

- [ ] If there are any new topics, new images, or major revisions, post a link in the docs channel in the public slack to publicize it.  You can post in the [`#docs` channel](https://ibm-cloud-success.slack.com/messages/C4G8V9GS1) and then repost as well in the [`#general` channel](https://ibm-cloud-success.slack.com/messages/C4G68BU7P) for greater visibility. Also the `#knative` channel.
