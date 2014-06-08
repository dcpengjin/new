new
===

what'snew_is _new
operation = 'list/';
database = 'organism';
organisms = urlread(strcat(base,operation,database));
organisms = regexpi(organisms,'[^\n]+','match')'; % convert to cellstr

% organisms is an array of cell strings, one for each organism in the KEGG taxonomic classification database. Find an entry with the string Homo sapiens and notice that the KEGG organism code for Homo sapiens is hsa.
%regexpi 是正则表达式，首先理解为在organisms 里面去寻找符合条件的字符，并且返回那些符合条件的字符的位置。
%具体的用法可以先找正则表达式的知识来学习。[^\n]+ 表示非空格，\n表示空格
% 关于正则表达式的知识很复杂，不过还是可以通过一些基本规则来进行学习： 
% 比如，正则表达式'Joh?n\w*'表示什么？表示Jo然后是可选的h，然后是n，然后是任意
%数量的字母，\w 表示字母，*表示任意数量。所以，Jon, John, Jonathan, Johnny
%都符合上述要求。

hsa_idx = find(~cellfun(@isempty,regexpi(organisms,'Homo sapiens')));
% cellfun是一个函数，目的是把@后面的函数用于，后面的cell格子里面的每个函数，比如这句话，就是把isempty用于regexpi(organisms,'Homo sapiens') 产生的每一个函数，而organisms又是 urlread直接产生的。
organisms(hsa_idx)
ans = 
'T01001	hsa	Homo sapiens (human)	Eukaryotes;Animals;Vertebrates;Mammals'
Get the list of pathways for Homo sapiens in KEGG PATHWAY database
operation = 'list/';
database = 'pathway/';
organismCode = 'hsa';
pathway_list = urlread(strcat(base,operation,database,organismCode));
pathway_list = regexpi(pathway_list,'[^\n]+','match')'; % convert to cellstr在这个地方，必须指出实际上新的数据库是全部在网上进行操作的。所谓查询命令，就是URL而已。
Get the total number of pathways.
num_pathways = numel(pathway_list)
num_pathways = 
278
