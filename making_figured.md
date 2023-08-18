## Making figures using ggvolc

After data is loaded in as a df it can be utilized by ggvolc. The most basic example:

	ggvolc(df)

You can make the same plot with 10 "attention genes" (a df of exactly 10 genes to display gene names for on the plot)
*It is important to note that the gene names, col_names, row_names, and data values must be identical for it to work*

	dggvolc(df, attention_genes)

Example "attention genes" df

| genes | baseMean | log2FoldChange | IfcSE | stat | pvalue | padj |
| ----- | -------- | -------------- | ----- | ---- | ------ | ---- |
| gene1 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene2 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene3 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene4 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene5 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene6 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene7 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene8 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene9 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|
| gene10 | 343.43 | -0.0344 | 0.45344 | -0.453954 | 0.98343 | 0.9364|

and send the results to the 'Run Selector' to view the four SRR accession numbers in one location.

| Run | Library name |
| --- | ------------ |
| SRR12830230 | Daptomycin-2 |
| SRR12830233 | UT-control-2 |
| SRR12830234 | Daptomycin-1 |
| SRR12830237 | UT-control-1 |

 Customize plot by increasing the point size by log2FoldChange and seqments based on the p-value

	ggvolc(df, attention_genes, size_var = "log2FoldChange", add_seg = TRUE)

 Customize plot by increasing the point size by log2FoldChange and seqments based on the p-value

	ggvolc(df, attention_genes, size_var = "pvalue", add_seg = TRUE)

 More customization! Color and specific thresholds
 
	gggvolc(
    df, 
    attention_genes,
    size_var = "pvalue",
    p_value = 0.05,
    fc = 1,
    not_sig_color = "grey82",
    down_reg_color = "#00798c",
    up_reg_color = "#d1495b",
    add_seg = FALSE
    )
