# Load the content of the uploaded Jupyter Notebook to analyze its structure and extract relevant information for the README.
import nbformat

# Path to the uploaded notebook
notebook_path = '/mnt/data/ECHOCARDIOGRAM.ipynb'

# Load the notebook content
with open(notebook_path, 'r') as f:
    notebook_content = nbformat.read(f, as_version=4)

# Extracting basic details like titles, markdown cells, and code cells
title = ""
markdown_cells = []
code_cells = []

for cell in notebook_content['cells']:
    if cell['cell_type'] == 'markdown':
        markdown_cells.append(cell['source'])
        if not title and "# " in cell['source']:
            # Assuming the first markdown title as the main title
            title = cell['source'].split("\n")[0].replace("#", "").strip()
    elif cell['cell_type'] == 'code':
        code_cells.append(cell['source'])

# Displaying the extracted title and a preview of the content
title, markdown_cells[:2], len(code_cells)  # Display title, first 2 markdown cells, and count of code cells
