## Colab Cheat Sheet

If you want to clone a repo and then open the notebooks inside it, the best way is to clone the repo into your Google Drive first.

Mount Drive:

```Python
from google.colab import drive
drive.mount('/content/drive')
```

Clone into Drive:

```Python
%cd /content/drive/MyDrive
!git clone https://github.com/username/repository.git
# replace the url with actual github repo url
```

Open Google Drive, locate the clone of GitHub repo, find the notebook file and open in Colab.

