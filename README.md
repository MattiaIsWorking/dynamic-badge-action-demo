# dynamic-badge-action-demo

![badge](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/MattiaIsWorking/3ee9cff571564854fe56ae14f7e5d2d6/raw/commits.json)

![badge](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/MattiaIsWorking/fae943e96001bebcf84a9a164f42d448/raw/lines.json)


## good to know

Two ways to access variables in workflows

```yml
 - name: Count commits
    run: echo "COUNT=$(git rev-list --count HEAD)" >> $GITHUB_ENV

- name: Create Awesome Badge
    uses: schneegans/dynamic-badges-action@v1.7.0
    with:
        auth: ${{ secrets.GIST_SECRET }}
        gistID: 3ee9cff571564854fe56ae14f7e5d2d6
        filename: commits.json
        label: Commits
        message: ${{ env.COUNT }}
        color: red
```


or 

```yml
- name: Lines of total code
    id: lines
    run: |
        echo "lines=$(find . -type f ! -path './.git/*' -print0 \
        | xargs -0 wc -l \
        | tail -n 1 \
        | awk '{print $1}')" >> $GITHUB_OUTPUT

- name: Create Awesome Badge
    uses: schneegans/dynamic-badges-action@v1.7.0
    with:
        auth: ${{ secrets.GIST_SECRET }}
        gistID: fae943e96001bebcf84a9a164f42d448
        filename: lines.json
        label: Lines of Code
        message: ${{ steps.lines.outputs.lines }}
        color: blue
```
