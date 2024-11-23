+++
title = '{{ replace .Name "-" " " | title }}'
date = {{ .Date }}
draft = false
aliases = ['{{ printf "%s/%s%s-alias/" site.LanguagePrefix .File.Dir .File.ContentBaseName}}']
+++
