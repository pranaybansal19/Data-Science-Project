# DataMindz — ChangeMyView analysis

This project contains the team's **CMV_Analysis** notebook and matching report: *What Changes a Mind? Length, Timing and Evidence on r/ChangeMyView*.

**Repository:** [pranaybansal19/Data-Science-Project](https://github.com/pranaybansal19/Data-Science-Project)

## Data sources

- **Archive download:** [Arctic Shift Reddit Download Tool](https://arctic-shift.photon-reddit.com/download-tool)
- **Community:** [r/ChangeMyView](https://www.reddit.com/r/changemyview/)

The raw `.zst` archives cover January 2013 through December 2025. This is the archive coverage; the filtered analysis and all reported hypothesis tests use posts from 1 April 2017 through 30 November 2022.

## Structure

```text
CSE558_CMV_FINAL/
  CMV_Analysis.ipynb      Complete analysis, explanations and saved outputs
  README.md              Setup and reproduction instructions
  requirements.txt       Notebook dependencies
  .gitignore             Excludes large archives and temporary files
  data/
    raw/
      changemyview_submissions.zst
      changemyview_comments.zst
  report/
    main.tex             LaTeX report source
    main.pdf             Compiled project report
    figures/
      op_award_share.png
      length.png
      delay_link.png
      post_length_award.png
```

There is one analysis notebook, with no separate processing scripts or JSON summaries. It builds the analysis tables directly from the raw archives.

## Run

1. Open this project folder in VS Code with Python and Jupyter support, or an existing Jupyter environment.
2. Install dependencies into the selected environment:

   ```powershell
   python -m pip install -r requirements.txt
   ```

3. Keep the two raw archives in [data/raw](data/raw). They are present locally but excluded from Git; a fresh checkout requires obtaining them separately.
4. Open [CMV_Analysis.ipynb](CMV_Analysis.ipynb), select the environment, and choose **Restart Kernel and Run All**.
5. Save the notebook to retain fresh results. The four figures used by the report are written to [report/figures](report/figures). The notebook may also regenerate an outlier-diagnostics image; that optional file is not needed for the report or submission.

The notebook accepts the project folder or its parent as its working directory. It scans the full comments archive and retains metadata for millions of records in memory; runtime and RAM use depend on the machine.

The notebook contains saved outputs from the complete analysis run. Re-running it from the raw archives reproduces the preparation pipeline, figures and statistical tests.

## Analysis flow

1. Read raw submissions and comments and normalize IDs.
2. Reconstruct OP delta awards from bot confirmations; credit an opening reply for an award to the same author later in its branch.
3. Filter to the April 2017–November 2022 window and eligible threads/replies.
4. Inspect missingness, duplicates, outliers and descriptive patterns.
5. Run four hypothesis tests: within-thread reply length, early versus late replies, linked versus unlinked replies, and original-post length by OP award status.

The results describe 479,276 replies from 25,439 represented threads for Tests 1–3 and 44,160 intact threads for Test 4.

## Compile the report

From [report](report), run:

```powershell
pdflatex main.tex
pdflatex main.tex
```

Alternatively, upload [main.tex](report/main.tex) and its `figures` folder to Overleaf. Running the notebook regenerates charts but does not update the numerical prose in the report or compile the PDF. Reconcile the report with fresh notebook outputs if analysis changes.

## Methodological notes

- Replies within a thread share an OP and context. The report treats reply-level proportion tests as observational and reports thread-level checks where available.
- Only claim hypotheses and meaningful-effect thresholds were specified before analysis if that is historically accurate.

The report separates statistical significance from practical effect size and states the main selection, dependence and outcome-measurement limitations.
