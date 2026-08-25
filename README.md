name: Generate Matrix Snake

on:
  schedule:
    - cron: "0 0 * * *"

  workflow_dispatch:

  push:
    branches:
      - main

jobs:
  generate-snake:
    permissions:
      contents: write

    runs-on: ubuntu-latest

    steps:
      - name: Generate Matrix Snake
        uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}

          outputs: |
            dist/github-contribution-grid-snake.svg?color_snake=%2339FF14&color_dots=%23062A12,%230B6E1E,%2300FF41,%2339FF14,%23FFFFFF

        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Push Snake to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
          commit_message: "chore: update matrix snake"

        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
