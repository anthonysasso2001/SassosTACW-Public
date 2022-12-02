# How to Export MS Word Sources to BibTex / Cther Citation managers Manually

Largely adopted from [this post on Zotero.org](https://www.zotero.org/support/kb/importing_formatted_bibliographies) but with slight additions for the final export part from step 4-9.

---

1. Go to [this website](https://gist.github.com/JaimeChavarriaga/40166befb14f2fe5dac390688d9eaf03)

2. Download the bibtex.xsl file and put it into
   1. **MS Word 2016/19/Office 365** \
		*"C:\Users\<currentusername>\AppData\Roaming\Microsoft\Bibliography\Style"*
   
   2. **MS Word 2010**\
		*"C:\Program Files\Microsoft Office\<Office version>\Bibliography\Style\"*
		*"C:\Program Files (x86)\Microsoft Office\<Office version>\Bibliography\Style"*
   
   3. **MS Word for Mac** \
		In "Show Package Contents” after R-Clicking app go to Content/Resources/Style.

3. Create an empty Word file and go to the resources tab, then add a bibliography and set style to bibtex export.

4. Click manage sources > click the top source > *"Shift + PgDn"* to highlight all sources, or select specific sources instead as needed.

5. Use the *"Copy ->"* to add all the citations the file and update bibliography to add citations (may take a while depending on how many were added).

6. Select the beginning of the first citation (should begin with @article) then *"Shift+PgDn"* until you have selected them all.

7. Copy and paste into a note file and save with .bib file type (I would name wordExport.bib or similar).

8. Import into citation manager of choice and sort into subfolders as needed.

9.  Cry.