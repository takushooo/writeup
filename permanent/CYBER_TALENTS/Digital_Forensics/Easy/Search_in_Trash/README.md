# Partition Lost
## 問題文

My HDD was destroyed in an accident. However, I was able to recover my recycle bin file . Can you know the flag ?

### 問題ファイル
```
wget https://s3-eu-west-1.amazonaws.com/hubchallenges/Forensics/search-trash
```

## FLAG

```
FLAG(701_L@b$_DR_DFIR)
```

## 解法
```
$ strings search-trash
:\ar.txt
:\ast.txt
:\az.txt
:\ba.txt
:\be.txt
:\bg.txt
:\bn.txt
:\br.txt
:\ca.txt
:\co.txt
:\cs.txt
:\cy.txt
:\da.txt
:\de.txt
:\el.txt
:\eo.txt
:\es.txt
:\et.txt
:\eu.txt
:\ext.txt
:\fa.txt
:\fi.txt
:\FLag{Fat_32_DF_2}.txt
:\fr.txt
:\fur.txt
:\fy.txt
:\ga.txt
:\gl.txt
:\gu.txt
:\he.txt
:\hi.txt
:\hr.txt
:\hu.txt
:\hy.txt
:\icuuc51.dll
:\id.txt
:\idriver.dll
:\ikernel.dll
:\io.txt
:\is.txt
:\IsoBuster.dll
:\it.txt
:\ja.txt
:\ka.txt
:\kaa.txt
:\kk.txt
:\ko.txt
:\ku.txt
:\ku-ckb.txt
:\ky.txt
:\libbfio.dll
:\lij.txt
:\LMS.dll
:\LMS-FS.dll
:\loader.exe.manifest
:\lt.txt
:\lv.txt
:\MD5Remote.dll
:\Microsoft.VC90.CRT.manifest
:\mk.txt
:\mn.txt
:\mng.txt
:\mng2.txt
:\mr.txt
:\ms.txt
:\msvcm90.dll
:\msvcp90.dll
:\msvcr90.dll
:\msvcr100.dll
H:\nb.txt
H:\ne.txt
H:\nl.txt
H:\nn.txt
H:\pa-in.txt
H:\PartitionWizard.exe.manifest
H:\pl.txt
H:\ps.txt
H:\pt.txt
H:\pt-br.txt
H:\QtCore4.dll
H:\QtGui4.dll
H:\QtNetwork4.dll
H:\ro.txt
H:\ru.txt
H:\sa.txt
H:\si.txt
H:\sk.txt
H:\sl.txt
H:\sq.txt
H:\sr-spc.txt
H:\sr-spl.txt
H:\sv.txt
H:\ta.txt
H:\th.txt
H:\tr.txt
H:\tt.txt
H:\ug.txt
H:\uk.txt
H:\uz.txt
H:\va.txt
H:\vi.txt
H:\yo.txt
```
FLAGげっと `FLag{Fat_32_DF_2}`
### reference
