## Critical rendering path:

- The critical rendering path is the `sequence of steps that browser goes` through to `convert HTML, CSS, JS into pixels` on the screen.

- Optimizing Critical render path `improves render performance`.

- The Critical Rendering path(CRP) includes Document Object Model(DOM), CSS Object model (CSSOM), render tree and layout.

- The `DOM is created` `after` `HTML is parsed `and the HTML may request Javascript which may `alter the DOM`.

- The HTML makes requests to `styles`, which in turn `builds the CSSOM`.

- The browser engine `combines the two` to create the Render tree.

- `Layout` determines the `size and location of everything on the page`.
- Once the layout is determined, `pixels are painted` on the screen.

### Document Object Model (DOM)

- DOM `construction` is `incremental`
- The `HTML response` turns into `tokens` which in turns into `nodes` and this will turn into `DOM tree`.
- A `single DOM node` starts with a `startTag token` and ends with an `endTag token`.
- `Nodes are connected into a DOM tree based on token hierarchy`.
- If another set of startTag and endTags come between a set of startTag and endTags (`you have a node inside a node`)

**The greater the number of nodes, the longer the following events in the CRP will take**

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/1cf0b0fb-0a15-4fda-96c6-3f1efe7b6a1c)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ee164d7c-a6cd-4ab9-b5cd-b815d95036c7)

---

#### CSS Object Model(CSSOM)

- When the DOM contains all the content of the page, the `CSSOM contains all the information on how to style the DOM`.

- CSSOM construction is `not Incremental` like DOM is incremental.

- CSS is render blocking - `the browser blocks page rendering until it receives and process all the CSS`.
