## 필요한 패키지 가져오기


```python
import os
import sys
import matplotlib as mpl
from matplotlib import font_manager
```


```python
# matplotlib의 폰트관리자를 통해 시스템 글꼴 폴더 확인
font_manager._rebuild()
```


```python
# 설정파일의 위치 조회
conf_file_path = mpl.matplotlib_fname()
conf_file_path
```




    'c:\\users\\administrator\\appdata\\local\\programs\\python\\python37\\lib\\site-packages\\matplotlib\\mpl-data\\matplotlibrc'




```python
# 설정파일이 들어있는 폴더
conf_file_dir = os.path.dirname(conf_file_path)
conf_file_dir
```




    'c:\\users\\administrator\\appdata\\local\\programs\\python\\python37\\lib\\site-packages\\matplotlib\\mpl-data'




```python
# 설정파일의 폴더 하위에 폰트파일이 위치해야 하는 폴더 경로 조회
font_path = conf_file_dir + "/fonts/ttf"
font_path
```




    'c:\\users\\administrator\\appdata\\local\\programs\\python\\python37\\lib\\site-packages\\matplotlib\\mpl-data/fonts/ttf'




```python
# 폰트 폴더를 열기 위한 명령어 수행
if sys.platform != "win32":
    font_path = font_path.replace("\\","/")
    command = 'open' + font_path
    os.system(command)
    quit()                                  
```


```python
# 윈도우는 운영체제의 글골 폴더 목록을 리스트로 가져온다
flist = font_manager.findSystemFonts(fontext='ttf')
flist
```




    ['C:\\Windows\\Fonts\\swisscbi.ttf',
     'C:\\WINDOWS\\Fonts\\calibrili.ttf',
     'C:\\Windows\\Fonts\\H2GTRM.TTF',
     'C:\\WINDOWS\\Fonts\\isocp2__.ttf',
     'C:\\Windows\\Fonts\\gadugib.ttf',
     'C:\\Windows\\Fonts\\H2HDRM.TTF',
     'C:\\WINDOWS\\Fonts\\comicz.ttf',
     'C:\\WINDOWS\\Fonts\\NirmalaB.ttf',
     'C:\\Windows\\Fonts\\NanumPen.ttf',
     'C:\\WINDOWS\\Fonts\\consolaz.ttf',
     'C:\\WINDOWS\\Fonts\\pala.ttf',
     'C:\\Windows\\Fonts\\Candara.ttf',
     'C:\\WINDOWS\\Fonts\\Candara.ttf',
     'C:\\WINDOWS\\Fonts\\swissck.ttf',
     'C:\\WINDOWS\\Fonts\\SymbM.ttf',
     'C:\\Windows\\Fonts\\segoeuii.ttf',
     'C:\\WINDOWS\\Fonts\\verdanab.ttf',
     'C:\\WINDOWS\\Fonts\\LeelUIsl.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareExtraBold.ttf',
     'C:\\WINDOWS\\Fonts\\taile.ttf',
     'C:\\WINDOWS\\Fonts\\timesbi.ttf',
     'C:\\Windows\\Fonts\\GENISO.ttf',
     'C:\\Windows\\Fonts\\HancomEQN.ttf',
     'C:\\WINDOWS\\Fonts\\swisscbi.ttf',
     'C:\\WINDOWS\\Fonts\\ARIALNBI.TTF',
     'C:\\WINDOWS\\Fonts\\msyh.ttc',
     'C:\\Windows\\Fonts\\dutchi.ttf',
     'C:\\Windows\\Fonts\\msyhl.ttc',
     'C:\\WINDOWS\\Fonts\\seguisbi.ttf',
     'C:\\WINDOWS\\Fonts\\couri.ttf',
     'C:\\Windows\\Fonts\\BKANT.TTF',
     'C:\\Windows\\Fonts\\mtproxy6.ttf',
     'C:\\Windows\\Fonts\\DUBAI-MEDIUM.TTF',
     'C:\\Windows\\Fonts\\AIGDT___.TTF',
     'C:\\Windows\\Fonts\\seguihis.ttf',
     'C:\\Windows\\Fonts\\ariali.ttf',
     'C:\\Windows\\Fonts\\cambriaz.ttf',
     'C:\\WINDOWS\\Fonts\\ANTQUAI.TTF',
     'C:\\Windows\\Fonts\\gothici_.ttf',
     'C:\\WINDOWS\\Fonts\\seguisb.ttf',
     'C:\\WINDOWS\\Fonts\\constani.ttf',
     'C:\\WINDOWS\\Fonts\\seguihis.ttf',
     'C:\\Windows\\Fonts\\symap___.ttf',
     'C:\\Windows\\Fonts\\NanumSquareExtraBold.ttf',
     'C:\\Windows\\Fonts\\NanumSquareRoundEB.ttf',
     'C:\\Windows\\Fonts\\GOTHICBI.TTF',
     'C:\\WINDOWS\\Fonts\\AMGDT___.ttf',
     'C:\\WINDOWS\\Fonts\\FiraCode-Retina.ttf',
     'C:\\WINDOWS\\Fonts\\simplex_.ttf',
     'C:\\Windows\\Fonts\\HanSantteutDotumBold.ttf',
     'C:\\Windows\\Fonts\\symath__.ttf',
     'C:\\Windows\\Fonts\\segoeui.ttf',
     'C:\\Windows\\Fonts\\syastro_.ttf',
     'C:\\Windows\\Fonts\\JUMJA.TTF',
     'C:\\Windows\\Fonts\\stylu.ttf',
     'C:\\WINDOWS\\Fonts\\NGULIM.TTF',
     'C:\\Windows\\Fonts\\micross.ttf',
     'C:\\WINDOWS\\Fonts\\micross.ttf',
     'C:\\Windows\\Fonts\\monbaiti.ttf',
     'C:\\WINDOWS\\Fonts\\ebrima.ttf',
     'C:\\Windows\\Fonts\\georgiai.ttf',
     'C:\\Windows\\Fonts\\comici.ttf',
     'C:\\WINDOWS\\Fonts\\D2CodingBold-Ver1.3-20171129.ttf',
     'C:\\WINDOWS\\Fonts\\himalaya.ttf',
     'C:\\WINDOWS\\Fonts\\D2Coding-Ver1.3-20171129.ttf',
     'C:\\WINDOWS\\Fonts\\BOOKOSBI.TTF',
     'C:\\Windows\\Fonts\\couri.ttf',
     'C:\\WINDOWS\\Fonts\\AcadEref.ttf',
     'C:\\WINDOWS\\Fonts\\Candaral.ttf',
     'C:\\WINDOWS\\Fonts\\isoct___.ttf',
     'C:\\Windows\\Fonts\\swissli.ttf',
     'C:\\Windows\\Fonts\\swissci.ttf',
     'C:\\WINDOWS\\Fonts\\DUBAI-REGULAR.TTF',
     'C:\\WINDOWS\\Fonts\\NanumSquareBold.ttf',
     'C:\\Windows\\Fonts\\techl___.ttf',
     'C:\\WINDOWS\\Fonts\\NanumGothic.ttf',
     'C:\\Windows\\Fonts\\segoeuisl.ttf',
     'C:\\Windows\\Fonts\\isocteui.ttf',
     'C:\\WINDOWS\\Fonts\\HanSantteutDotumRegular.ttf',
     'C:\\Windows\\Fonts\\corbel.ttf',
     'C:\\WINDOWS\\Fonts\\romand__.ttf',
     'C:\\Windows\\Fonts\\seguisym.ttf',
     'C:\\WINDOWS\\Fonts\\comicbd.ttf',
     'C:\\Windows\\Fonts\\times.ttf',
     'C:\\WINDOWS\\Fonts\\segoeuib.ttf',
     'C:\\WINDOWS\\Fonts\\YuGothM.ttc',
     'C:\\Windows\\Fonts\\Hancom Gothic Regular.ttf',
     'C:\\WINDOWS\\Fonts\\georgiaz.ttf',
     'C:\\Windows\\Fonts\\REFSAN.TTF',
     'C:\\Windows\\Fonts\\trebucit.ttf',
     'C:\\WINDOWS\\Fonts\\YuGothR.ttc',
     'C:\\Windows\\Fonts\\FiraCode-Light.ttf',
     'C:\\WINDOWS\\Fonts\\monosb.ttf',
     'C:\\WINDOWS\\Fonts\\ANTQUAB.TTF',
     'C:\\WINDOWS\\Fonts\\DUBAI-BOLD.TTF',
     'C:\\Windows\\Fonts\\NirmalaB.ttf',
     'C:\\WINDOWS\\Fonts\\isocpeui.ttf',
     'C:\\WINDOWS\\Fonts\\swisscb.ttf',
     'C:\\Windows\\Fonts\\H2PORL.TTF',
     'C:\\WINDOWS\\Fonts\\verdanai.ttf',
     'C:\\WINDOWS\\Fonts\\NanumBarunGothicLight.ttf',
     'C:\\WINDOWS\\Fonts\\consolai.ttf',
     'C:\\Windows\\Fonts\\eurro___.ttf',
     'C:\\Windows\\Fonts\\romab___.ttf',
     'C:\\WINDOWS\\Fonts\\ntailu.ttf',
     'C:\\WINDOWS\\Fonts\\swissli.ttf',
     'C:\\Windows\\Fonts\\romans__.ttf',
     'C:\\Windows\\Fonts\\swisscki.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareRoundR.ttf',
     'C:\\WINDOWS\\Fonts\\isoct2__.ttf',
     'C:\\WINDOWS\\Fonts\\YuGothL.ttc',
     'C:\\Windows\\Fonts\\swisscb.ttf',
     'C:\\Windows\\Fonts\\malgunbd_0.ttf',
     'C:\\Windows\\Fonts\\holomdl2.ttf',
     'C:\\WINDOWS\\Fonts\\palab.ttf',
     'C:\\WINDOWS\\Fonts\\HancomEQN.ttf',
     'C:\\Windows\\Fonts\\HANBatangExt.ttf',
     'C:\\Windows\\Fonts\\greekc__.ttf',
     'C:\\WINDOWS\\Fonts\\eurro___.ttf',
     'C:\\WINDOWS\\Fonts\\syastro_.ttf',
     'C:\\WINDOWS\\Fonts\\GOTHICB.TTF',
     'C:\\WINDOWS\\Fonts\\HanSantteutDotum-Bold.ttf',
     'C:\\Windows\\Fonts\\isocteur.ttf',
     'C:\\Windows\\Fonts\\Candarai.ttf',
     'C:\\Windows\\Fonts\\tahoma.ttf',
     'C:\\WINDOWS\\Fonts\\BOOKOSB.TTF',
     'C:\\WINDOWS\\Fonts\\trebucbi.ttf',
     'C:\\WINDOWS\\Fonts\\romanc__.ttf',
     'C:\\Windows\\Fonts\\arial.ttf',
     'C:\\Windows\\Fonts\\GARABD.TTF',
     'C:\\WINDOWS\\Fonts\\impact.ttf',
     'C:\\Windows\\Fonts\\monotxt_.ttf',
     'C:\\Windows\\Fonts\\constanz.ttf',
     'C:\\Windows\\Fonts\\WINGDNG2.TTF',
     'C:\\WINDOWS\\Fonts\\arialbi.ttf',
     'C:\\WINDOWS\\Fonts\\D2Coding-Ver1.3-20171129.ttc',
     'C:\\WINDOWS\\Fonts\\FiraCode-Regular.ttf',
     'C:\\Windows\\Fonts\\consolai.ttf',
     'C:\\Windows\\Fonts\\HANDotum.ttf',
     'C:\\Windows\\Fonts\\cambriai.ttf',
     'C:\\WINDOWS\\Fonts\\NanumBrush.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Dotum Light.ttf',
     'C:\\WINDOWS\\Fonts\\calibriz.ttf',
     'C:\\Windows\\Fonts\\taileb.ttf',
     'C:\\Windows\\Fonts\\NanumSquareRegular.ttf',
     'C:\\Windows\\Fonts\\palai.ttf',
     'C:\\Windows\\Fonts\\simsunb.ttf',
     'C:\\Windows\\Fonts\\techb___.ttf',
     'C:\\WINDOWS\\Fonts\\bgothm.ttf',
     'C:\\Windows\\Fonts\\mtproxy1.ttf',
     'C:\\Windows\\Fonts\\BOOKOSB.TTF',
     'C:\\Windows\\Fonts\\Candarali.ttf',
     'C:\\Windows\\Fonts\\swiss.ttf',
     'C:\\WINDOWS\\Fonts\\CoureI.ttf',
     'C:\\WINDOWS\\Fonts\\NanumMyeongjoExtraBold.ttf',
     'C:\\Windows\\Fonts\\isocpeur.ttf',
     'C:\\Windows\\Fonts\\LeelUIsl.ttf',
     'C:\\Windows\\Fonts\\ebrima.ttf',
     'C:\\WINDOWS\\Fonts\\techl___.ttf',
     'C:\\WINDOWS\\Fonts\\ariali.ttf',
     'C:\\WINDOWS\\Fonts\\BOOKOSI.TTF',
     'C:\\WINDOWS\\Fonts\\msjhl.ttc',
     'C:\\Windows\\Fonts\\WINGDNG3.TTF',
     'C:\\WINDOWS\\Fonts\\swissc.ttf',
     'C:\\Windows\\Fonts\\DUBAI-REGULAR.TTF',
     'C:\\Windows\\Fonts\\H2MKPB.TTF',
     'C:\\Windows\\Fonts\\malgunsl_0.ttf',
     'C:\\Windows\\Fonts\\calibrii.ttf',
     'C:\\Windows\\Fonts\\greeks__.ttf',
     'C:\\Windows\\Fonts\\HANBatang.ttf',
     'C:\\Windows\\Fonts\\swissi.ttf',
     'C:\\Windows\\Fonts\\NanumMyeongjoExtraBold.ttf',
     'C:\\Windows\\Fonts\\SymbP.ttf',
     'C:\\WINDOWS\\Fonts\\cityb___.ttf',
     'C:\\WINDOWS\\Fonts\\swiss.ttf',
     'C:\\Windows\\Fonts\\GOTHIC.TTF',
     'C:\\Windows\\Fonts\\cambria.ttc',
     'C:\\WINDOWS\\Fonts\\mtproxy8.ttf',
     'C:\\Windows\\Fonts\\italicc_.ttf',
     'C:\\WINDOWS\\Fonts\\AIGDT___.TTF',
     'C:\\WINDOWS\\Fonts\\swissb.ttf',
     'C:\\WINDOWS\\Fonts\\swisscbo.ttf',
     'C:\\WINDOWS\\Fonts\\wingding.ttf',
     'C:\\Windows\\Fonts\\NanumMyeongjo.ttf',
     'C:\\Windows\\Fonts\\swisscbo.ttf',
     'C:\\WINDOWS\\Fonts\\dutchbi.ttf',
     'C:\\WINDOWS\\Fonts\\gdt_____.ttf',
     'C:\\WINDOWS\\Fonts\\bgothl.ttf',
     'C:\\Windows\\Fonts\\verdanai.ttf',
     'C:\\Windows\\Fonts\\NanumBarunGothicUltraLight.ttf',
     'C:\\WINDOWS\\Fonts\\comsc.ttf',
     'C:\\Windows\\Fonts\\mingliub.ttc',
     'C:\\WINDOWS\\Fonts\\GARA.TTF',
     'C:\\WINDOWS\\Fonts\\HANDotum.ttf',
     'C:\\Windows\\Fonts\\REFSPCL.TTF',
     'C:\\Windows\\Fonts\\sanssbo_.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy6.ttf',
     'C:\\Windows\\Fonts\\dutchbi.ttf',
     'C:\\Windows\\Fonts\\romanc__.ttf',
     'C:\\WINDOWS\\Fonts\\H2MJRE.TTF',
     'C:\\Windows\\Fonts\\verdana.ttf',
     'C:\\WINDOWS\\Fonts\\swissbo.ttf',
     'C:\\Windows\\Fonts\\NanumGothicBold.ttf',
     'C:\\WINDOWS\\Fonts\\BKANT.TTF',
     'C:\\WINDOWS\\Fonts\\courbd.ttf',
     'C:\\WINDOWS\\Fonts\\isocteur.ttf',
     'C:\\Windows\\Fonts\\italic__.ttf',
     'C:\\WINDOWS\\Fonts\\FiraCode-Medium.ttf',
     'C:\\Windows\\Fonts\\georgia.ttf',
     'C:\\WINDOWS\\Fonts\\WINGDNG3.TTF',
     'C:\\WINDOWS\\Fonts\\NanumBarunpenRegular.ttf',
     'C:\\WINDOWS\\Fonts\\holomdl2.ttf',
     'C:\\Windows\\Fonts\\isoct___.ttf',
     'C:\\WINDOWS\\Fonts\\NanumGothicExtraBold.ttf',
     'C:\\WINDOWS\\Fonts\\batang.ttc',
     'C:\\WINDOWS\\Fonts\\romantic.ttf',
     'C:\\Windows\\Fonts\\SitkaZ.ttc',
     'C:\\WINDOWS\\Fonts\\msgothic.ttc',
     'C:\\Windows\\Fonts\\NanumBarunpenBold.ttf',
     'C:\\WINDOWS\\Fonts\\Candaraz.ttf',
     'C:\\WINDOWS\\Fonts\\dutcheb.ttf',
     'C:\\WINDOWS\\Fonts\\vinet.ttf',
     'C:\\Windows\\Fonts\\swissc.ttf',
     'C:\\Windows\\Fonts\\NanumGothicLight.ttf',
     'C:\\WINDOWS\\Fonts\\Hancom Gothic Regular.ttf',
     'C:\\Windows\\Fonts\\umath.ttf',
     'C:\\WINDOWS\\Fonts\\supef___.ttf',
     'C:\\Windows\\Fonts\\AMGDT___.ttf',
     'C:\\Windows\\Fonts\\NanumBarunGothicBold.ttf',
     'C:\\Windows\\Fonts\\segoesc.ttf',
     'C:\\WINDOWS\\Fonts\\trebucit.ttf',
     'C:\\WINDOWS\\Fonts\\ARIALNI.TTF',
     'C:\\WINDOWS\\Fonts\\malgunsl.ttf',
     'C:\\WINDOWS\\Fonts\\swissk.ttf',
     'C:\\WINDOWS\\Fonts\\swissci.ttf',
     'C:\\WINDOWS\\Fonts\\stylu.ttf',
     'C:\\Windows\\Fonts\\NirmalaS.ttf',
     'C:\\WINDOWS\\Fonts\\malgunbd.ttf',
     'C:\\WINDOWS\\Fonts\\NanumMyeongjo.ttf',
     'C:\\WINDOWS\\Fonts\\LeelawUI.ttf',
     'C:\\WINDOWS\\Fonts\\CoureBI.ttf',
     'C:\\WINDOWS\\Fonts\\H2PORL.TTF',
     'C:\\WINDOWS\\Fonts\\georgiai.ttf',
     'C:\\WINDOWS\\Fonts\\Candarali.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Dotum Bold.ttf',
     'C:\\WINDOWS\\Fonts\\HANBatangExt.ttf',
     'C:\\Windows\\Fonts\\consolaz.ttf',
     'C:\\WINDOWS\\Fonts\\seguiemj.ttf',
     'C:\\WINDOWS\\Fonts\\cambriai.ttf',
     'C:\\WINDOWS\\Fonts\\phagspa.ttf',
     'C:\\Windows\\Fonts\\mtproxy3.ttf',
     'C:\\WINDOWS\\Fonts\\CoureB.ttf',
     'C:\\Windows\\Fonts\\HATTEN.TTF',
     'C:\\Windows\\Fonts\\seguibl.ttf',
     'C:\\WINDOWS\\Fonts\\HMFMOLD.TTF',
     'C:\\Windows\\Fonts\\mtproxy9.ttf',
     'C:\\WINDOWS\\Fonts\\NanumBarunGothicUltraLight.ttf',
     'C:\\Windows\\Fonts\\NanumMyeongjoBold.ttf',
     'C:\\WINDOWS\\Fonts\\corbel.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy9.ttf',
     'C:\\Windows\\Fonts\\HMKMRHD.TTF',
     'C:\\Windows\\Fonts\\malgunbd.ttf',
     'C:\\Windows\\Fonts\\NanumSquareRoundR.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareLight.ttf',
     'C:\\WINDOWS\\Fonts\\segmdl2.ttf',
     'C:\\WINDOWS\\Fonts\\corbell.ttf',
     'C:\\WINDOWS\\Fonts\\HANBatangB.ttf',
     'C:\\WINDOWS\\Fonts\\consolab.ttf',
     'C:\\Windows\\Fonts\\BOOKOSI.TTF',
     'C:\\Windows\\Fonts\\Inkfree.ttf',
     'C:\\WINDOWS\\Fonts\\SitkaZ.ttc',
     'C:\\WINDOWS\\Fonts\\dutchi.ttf',
     'C:\\Windows\\Fonts\\framdit.ttf',
     'C:\\WINDOWS\\Fonts\\malgun_0.ttf',
     'C:\\WINDOWS\\Fonts\\bahnschrift.ttf',
     'C:\\WINDOWS\\Fonts\\verdana.ttf',
     'C:\\Windows\\Fonts\\CoureI.ttf',
     'C:\\Windows\\Fonts\\seguisli.ttf',
     'C:\\WINDOWS\\Fonts\\ntailub.ttf',
     'C:\\Windows\\Fonts\\swissb.ttf',
     'C:\\Windows\\Fonts\\ntailub.ttf',
     'C:\\Windows\\Fonts\\ARIALNBI.TTF',
     'C:\\Windows\\Fonts\\NanumBarunGothicLight.ttf',
     'C:\\Windows\\Fonts\\NanumGothic.ttf',
     'C:\\Windows\\Fonts\\arialbd.ttf',
     'C:\\Windows\\Fonts\\malgunsl.ttf',
     'C:\\WINDOWS\\Fonts\\HYHWPEQ.TTF',
     'C:\\Windows\\Fonts\\BOOKOS.TTF',
     'C:\\Windows\\Fonts\\monosbi.ttf',
     'C:\\Windows\\Fonts\\sanss___.ttf',
     'C:\\Windows\\Fonts\\verdanaz.ttf',
     'C:\\Windows\\Fonts\\comsc.ttf',
     'C:\\WINDOWS\\Fonts\\segoeprb.ttf',
     'C:\\WINDOWS\\Fonts\\SymbC.ttf',
     'C:\\WINDOWS\\Fonts\\HMKMRHD.TTF',
     'C:\\Windows\\Fonts\\H2MJSM.TTF',
     'C:\\WINDOWS\\Fonts\\NanumSquareRoundEB.ttf',
     'C:\\Windows\\Fonts\\NanumBarunGothic.ttf',
     'C:\\WINDOWS\\Fonts\\swisscl.ttf',
     'C:\\Windows\\Fonts\\courbi.ttf',
     'C:\\WINDOWS\\Fonts\\sanssbo_.ttf',
     'C:\\Windows\\Fonts\\FiraCode-Medium.ttf',
     'C:\\WINDOWS\\Fonts\\HANWing2.ttf',
     'C:\\WINDOWS\\Fonts\\seguisli.ttf',
     'C:\\WINDOWS\\Fonts\\monosi.ttf',
     'C:\\Windows\\Fonts\\HMKMMAG.TTF',
     'C:\\Windows\\Fonts\\segoepr.ttf',
     'C:\\Windows\\Fonts\\eurr____.ttf',
     'C:\\Windows\\Fonts\\simplex_.ttf',
     'C:\\WINDOWS\\Fonts\\isocp3__.ttf',
     'C:\\Windows\\Fonts\\D2CodingBold-Ver1.3-20171129.ttf',
     'C:\\WINDOWS\\Fonts\\times.ttf',
     'C:\\Windows\\Fonts\\isocp3__.ttf',
     'C:\\Windows\\Fonts\\NGULIM.TTF',
     'C:\\Windows\\Fonts\\georgiab.ttf',
     'C:\\WINDOWS\\Fonts\\eurr____.ttf',
     'C:\\Windows\\Fonts\\HMFMMUEX.TTC',
     'C:\\WINDOWS\\Fonts\\greeks__.ttf',
     'C:\\WINDOWS\\Fonts\\romans__.ttf',
     'C:\\Windows\\Fonts\\Gabriola.ttf',
     'C:\\Windows\\Fonts\\NanumSquareRoundL.ttf',
     'C:\\WINDOWS\\Fonts\\framd.ttf',
     'C:\\Windows\\Fonts\\gothicg_.ttf',
     'C:\\Windows\\Fonts\\ARIALNI.TTF',
     'C:\\WINDOWS\\Fonts\\mingliub.ttc',
     'C:\\WINDOWS\\Fonts\\JUMJA.TTF',
     'C:\\WINDOWS\\Fonts\\malgun.ttf',
     'C:\\Windows\\Fonts\\나눔고딕코딩.ttf',
     'C:\\Windows\\Fonts\\trebucbd.ttf',
     'C:\\Windows\\Fonts\\isoct3__.ttf',
     'C:\\Windows\\Fonts\\dutcheb.ttf',
     'C:\\Windows\\Fonts\\romand__.ttf',
     'C:\\WINDOWS\\Fonts\\HANBatangExtB.ttf',
     'C:\\WINDOWS\\Fonts\\msjh.ttc',
     'C:\\Windows\\Fonts\\himalaya.ttf',
     'C:\\Windows\\Fonts\\segmdl2.ttf',
     'C:\\Windows\\Fonts\\bgothm.ttf',
     'C:\\WINDOWS\\Fonts\\simsun.ttc',
     'C:\\WINDOWS\\Fonts\\javatext.ttf',
     'C:\\WINDOWS\\Fonts\\counb___.ttf',
     'C:\\Windows\\Fonts\\D2Coding-Ver1.3-20171129.ttc',
     'C:\\Windows\\Fonts\\scriptc_.ttf',
     'C:\\WINDOWS\\Fonts\\calibril.ttf',
     'C:\\Windows\\Fonts\\wingding.ttf',
     'C:\\Windows\\Fonts\\FiraCode-Bold.ttf',
     'C:\\Windows\\Fonts\\constan.ttf',
     'C:\\Windows\\Fonts\\isoct2__.ttf',
     'C:\\WINDOWS\\Fonts\\phagspab.ttf',
     'C:\\WINDOWS\\Fonts\\scripts_.ttf',
     'C:\\Windows\\Fonts\\H2GTRE.TTF',
     'C:\\WINDOWS\\Fonts\\NanumGothicLight.ttf',
     'C:\\Windows\\Fonts\\KoPub Batang Medium.ttf',
     'C:\\Windows\\Fonts\\italict_.ttf',
     'C:\\WINDOWS\\Fonts\\YuGothB.ttc',
     'C:\\Windows\\Fonts\\HanSantteutDotumRegular.ttf',
     'C:\\Windows\\Fonts\\batang.ttc',
     'C:\\WINDOWS\\Fonts\\cambriab.ttf',
     'C:\\Windows\\Fonts\\msjhbd.ttc',
     'C:\\WINDOWS\\Fonts\\comic.ttf',
     'C:\\WINDOWS\\Fonts\\corbelz.ttf',
     'C:\\Windows\\Fonts\\segoeuib.ttf',
     'C:\\Windows\\Fonts\\malgun_0.ttf',
     'C:\\WINDOWS\\Fonts\\seguibli.ttf',
     'C:\\WINDOWS\\Fonts\\italic__.ttf',
     'C:\\WINDOWS\\Fonts\\mvboli.ttf',
     'C:\\Windows\\Fonts\\H2MJRE.TTF',
     'C:\\Windows\\Fonts\\gulim.ttc',
     'C:\\WINDOWS\\Fonts\\HANBatangExtBB.ttf',
     'C:\\WINDOWS\\Fonts\\seguili.ttf',
     'C:\\Windows\\Fonts\\msgothic.ttc',
     'C:\\Windows\\Fonts\\pala.ttf',
     'C:\\WINDOWS\\Fonts\\comici.ttf',
     'C:\\WINDOWS\\Fonts\\webdings.ttf',
     'C:\\WINDOWS\\Fonts\\symeteo_.ttf',
     'C:\\Windows\\Fonts\\swissek.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareRegular.ttf',
     'C:\\Windows\\Fonts\\monosi.ttf',
     'C:\\Windows\\Fonts\\HANWing2.ttf',
     'C:\\WINDOWS\\Fonts\\sansso__.ttf',
     'C:\\Windows\\Fonts\\seguiemj.ttf',
     'C:\\WINDOWS\\Fonts\\gothici_.ttf',
     'C:\\Windows\\Fonts\\NanumGothicExtraBold.ttf',
     'C:\\WINDOWS\\Fonts\\msyhl.ttc',
     'C:\\Windows\\Fonts\\palab.ttf',
     'C:\\Windows\\Fonts\\ANTQUAI.TTF',
     'C:\\WINDOWS\\Fonts\\calibri.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Dotum Medium.ttf',
     'C:\\WINDOWS\\Fonts\\malgunsl_0.ttf',
     'C:\\WINDOWS\\Fonts\\gothicg_.ttf',
     'C:\\WINDOWS\\Fonts\\swissbi.ttf',
     'C:\\Windows\\Fonts\\나눔고딕코딩-Bold.ttf',
     'C:\\Windows\\Fonts\\simsun.ttc',
     'C:\\WINDOWS\\Fonts\\swissl.ttf',
     'C:\\Windows\\Fonts\\HANDotumB.ttf',
     'C:\\WINDOWS\\Fonts\\Hancom Gothic Bold.ttf',
     'C:\\WINDOWS\\Fonts\\Coure.ttf',
     'C:\\Windows\\Fonts\\segoeuiz.ttf',
     'C:\\WINDOWS\\Fonts\\swisse.ttf',
     'C:\\WINDOWS\\Fonts\\NanumBarunGothicBold.ttf',
     'C:\\WINDOWS\\Fonts\\ebrimabd.ttf',
     'C:\\Windows\\Fonts\\scripts_.ttf',
     'C:\\WINDOWS\\Fonts\\HMKMMAG.TTF',
     'C:\\Windows\\Fonts\\YuGothM.ttc',
     'C:\\WINDOWS\\Fonts\\DUBAI-LIGHT.TTF',
     'C:\\Windows\\Fonts\\panroman.ttf',
     'C:\\WINDOWS\\Fonts\\umath.ttf',
     'C:\\Windows\\Fonts\\sylfaen.ttf',
     'C:\\WINDOWS\\Fonts\\H2GPRM.TTF',
     'C:\\Windows\\Fonts\\dutch.ttf',
     'C:\\Windows\\Fonts\\swisse.ttf',
     'C:\\Windows\\Fonts\\sanssb__.ttf',
     'C:\\Windows\\Fonts\\arialbi.ttf',
     'C:\\WINDOWS\\Fonts\\lucon.ttf',
     'C:\\WINDOWS\\Fonts\\isoct3__.ttf',
     'C:\\Windows\\Fonts\\HMKMAMI.TTF',
     'C:\\Windows\\Fonts\\ntailu.ttf',
     'C:\\WINDOWS\\Fonts\\constanz.ttf',
     'C:\\Windows\\Fonts\\mtproxy5.ttf',
     'C:\\WINDOWS\\Fonts\\symath__.ttf',
     'C:\\Windows\\Fonts\\Hancom Gothic Bold.ttf',
     'C:\\WINDOWS\\Fonts\\segoeuil.ttf',
     'C:\\WINDOWS\\Fonts\\나눔고딕코딩.ttf',
     'C:\\Windows\\Fonts\\ANTQUAB.TTF',
     'C:\\WINDOWS\\Fonts\\georgiab.ttf',
     'C:\\WINDOWS\\Fonts\\Candarai.ttf',
     'C:\\WINDOWS\\Fonts\\H2MJSM.TTF',
     'C:\\Windows\\Fonts\\mtproxy8.ttf',
     'C:\\WINDOWS\\Fonts\\marlett.ttf',
     'C:\\WINDOWS\\Fonts\\sanss___.ttf',
     'C:\\Windows\\Fonts\\javatext.ttf',
     'C:\\Windows\\Fonts\\Coure.ttf',
     'C:\\Windows\\Fonts\\bgothl.ttf',
     'C:\\Windows\\Fonts\\KoPub Batang Bold.ttf',
     'C:\\Windows\\Fonts\\swisski.ttf',
     'C:\\Windows\\Fonts\\FiraCode-Regular.ttf',
     'C:\\WINDOWS\\Fonts\\segoeuiz.ttf',
     'C:\\Windows\\Fonts\\YuGothL.ttc',
     'C:\\Windows\\Fonts\\technic_.ttf',
     'C:\\WINDOWS\\Fonts\\taileb.ttf',
     'C:\\Windows\\Fonts\\corbelb.ttf',
     'C:\\Windows\\Fonts\\isocpeui.ttf',
     'C:\\Windows\\Fonts\\comicbd.ttf',
     'C:\\Windows\\Fonts\\calibrili.ttf',
     'C:\\WINDOWS\\Fonts\\swisscki.ttf',
     'C:\\WINDOWS\\Fonts\\cour.ttf',
     'C:\\Windows\\Fonts\\mmrtext.ttf',
     'C:\\WINDOWS\\Fonts\\msjhbd.ttc',
     'C:\\Windows\\Fonts\\swissbo.ttf',
     'C:\\Windows\\Fonts\\KoPub Dotum Light.ttf',
     'C:\\Windows\\Fonts\\HYHWPEQ.TTF',
     'C:\\Windows\\Fonts\\comic.ttf',
     'C:\\Windows\\Fonts\\SitkaI.ttc',
     'C:\\WINDOWS\\Fonts\\HMKMAMI.TTF',
     'C:\\Windows\\Fonts\\cambriab.ttf',
     'C:\\WINDOWS\\Fonts\\ARIALN.TTF',
     'C:\\WINDOWS\\Fonts\\framdit.ttf',
     'C:\\WINDOWS\\Fonts\\H2MKPB.TTF',
     'C:\\WINDOWS\\Fonts\\timesbd.ttf',
     'C:\\Windows\\Fonts\\Candarab.ttf',
     'C:\\Windows\\Fonts\\impact.ttf',
     'C:\\Windows\\Fonts\\NanumSquareBold.ttf',
     'C:\\WINDOWS\\Fonts\\HANDotumExt.ttf',
     'C:\\Windows\\Fonts\\mvboli.ttf',
     'C:\\Windows\\Fonts\\constani.ttf',
     'C:\\WINDOWS\\Fonts\\courbi.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareRoundB.ttf',
     'C:\\WINDOWS\\Fonts\\HANBatang.ttf',
     'C:\\Windows\\Fonts\\msjhl.ttc',
     'C:\\Windows\\Fonts\\txt_____.ttf',
     'C:\\Windows\\Fonts\\symbol.ttf',
     'C:\\WINDOWS\\Fonts\\arialbd.ttf',
     'C:\\Windows\\Fonts\\dutchb.ttf',
     'C:\\Windows\\Fonts\\swissel.ttf',
     'C:\\WINDOWS\\Fonts\\malgunbd_0.ttf',
     'C:\\Windows\\Fonts\\HANDotumExt.ttf',
     'C:\\Windows\\Fonts\\corbelz.ttf',
     'C:\\Windows\\Fonts\\H2PORM.TTF',
     'C:\\Windows\\Fonts\\seguisb.ttf',
     'C:\\Windows\\Fonts\\gothice_.ttf',
     'C:\\WINDOWS\\Fonts\\txt_____.ttf',
     'C:\\Windows\\Fonts\\ebrimabd.ttf',
     'C:\\Windows\\Fonts\\HMFMPYUN.TTF',
     'C:\\WINDOWS\\Fonts\\FiraCode-Bold.ttf',
     'C:\\Windows\\Fonts\\msjh.ttc',
     'C:\\WINDOWS\\Fonts\\GENISO.ttf',
     'C:\\WINDOWS\\Fonts\\consola.ttf',
     'C:\\WINDOWS\\Fonts\\tahoma.ttf',
     'C:\\WINDOWS\\Fonts\\techb___.ttf',
     'C:\\WINDOWS\\Fonts\\symap___.ttf',
     'C:\\WINDOWS\\Fonts\\segoeuii.ttf',
     'C:\\WINDOWS\\Fonts\\msyi.ttf',
     'C:\\Windows\\Fonts\\lucon.ttf',
     'C:\\WINDOWS\\Fonts\\ANTQUABI.TTF',
     'C:\\Windows\\Fonts\\SitkaB.ttc',
     'C:\\Windows\\Fonts\\compi.ttf',
     'C:\\WINDOWS\\Fonts\\segoepr.ttf',
     'C:\\WINDOWS\\Fonts\\GOTHIC.TTF',
     'C:\\Windows\\Fonts\\framd.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy3.ttf',
     'C:\\Windows\\Fonts\\segoeprb.ttf',
     'C:\\Windows\\Fonts\\timesi.ttf',
     'C:\\WINDOWS\\Fonts\\swissi.ttf',
     'C:\\WINDOWS\\Fonts\\corbeli.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy4.ttf',
     'C:\\WINDOWS\\Fonts\\ARIALNB.TTF',
     'C:\\Windows\\Fonts\\sansso__.ttf',
     'C:\\WINDOWS\\Fonts\\Gabriola.ttf',
     'C:\\Windows\\Fonts\\NanumBarunpenRegular.ttf',
     'C:\\WINDOWS\\Fonts\\romant__.ttf',
     'C:\\WINDOWS\\Fonts\\trebucbd.ttf',
     'C:\\WINDOWS\\Fonts\\DUBAI-MEDIUM.TTF',
     'C:\\Windows\\Fonts\\symeteo_.ttf',
     'C:\\WINDOWS\\Fonts\\symbol.ttf',
     'C:\\Windows\\Fonts\\gdt_____.ttf',
     'C:\\Windows\\Fonts\\GOTHICB.TTF',
     'C:\\WINDOWS\\Fonts\\SitkaB.ttc',
     'C:\\Windows\\Fonts\\mtproxy7.ttf',
     'C:\\Windows\\Fonts\\SymbM.ttf',
     'C:\\Windows\\Fonts\\romantic.ttf',
     'C:\\Windows\\Fonts\\seguibli.ttf',
     'C:\\Windows\\Fonts\\symusic_.ttf',
     'C:\\WINDOWS\\Fonts\\gothice_.ttf',
     'C:\\Windows\\Fonts\\malgun.ttf',
     'C:\\WINDOWS\\Fonts\\trebuc.ttf',
     'C:\\WINDOWS\\Fonts\\complex_.ttf',
     'C:\\Windows\\Fonts\\AcadEref.ttf',
     'C:\\WINDOWS\\Fonts\\FiraCode-Light.ttf',
     'C:\\Windows\\Fonts\\swissbi.ttf',
     'C:\\Windows\\Fonts\\KoPub Dotum Bold.ttf',
     'C:\\WINDOWS\\Fonts\\isocteui.ttf',
     'C:\\WINDOWS\\Fonts\\monosbi.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy1.ttf',
     'C:\\Windows\\Fonts\\calibrib.ttf',
     'C:\\Windows\\Fonts\\D2Coding-Ver1.3-20171129.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Batang Bold.ttf',
     'C:\\Windows\\Fonts\\ARIALN.TTF',
     'C:\\Windows\\Fonts\\phagspab.ttf',
     'C:\\Windows\\Fonts\\msyhbd.ttc',
     'C:\\Windows\\Fonts\\timesbi.ttf',
     'C:\\WINDOWS\\Fonts\\HanSantteutDotumBold.ttf',
     'C:\\WINDOWS\\Fonts\\compi.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy5.ttf',
     'C:\\WINDOWS\\Fonts\\NanumBarunGothic.ttf',
     'C:\\WINDOWS\\Fonts\\swisski.ttf',
     'C:\\Windows\\Fonts\\CENTURY.TTF',
     'C:\\Windows\\Fonts\\Candaral.ttf',
     'C:\\WINDOWS\\Fonts\\sylfaen.ttf',
     'C:\\Windows\\Fonts\\swissl.ttf',
     'C:\\WINDOWS\\Fonts\\H2GTRM.TTF',
     'C:\\Windows\\Fonts\\LeelaUIb.ttf',
     'C:\\Windows\\Fonts\\H2SA1M.TTF',
     'C:\\Windows\\Fonts\\constanb.ttf',
     'C:\\Windows\\Fonts\\phagspa.ttf',
     'C:\\WINDOWS\\Fonts\\technic_.ttf',
     'C:\\Windows\\Fonts\\swissck.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Batang Medium.ttf',
     'C:\\WINDOWS\\Fonts\\NanumMyeongjoBold.ttf',
     'C:\\WINDOWS\\Fonts\\scriptc_.ttf',
     'C:\\WINDOWS\\Fonts\\tahomabd.ttf',
     'C:\\WINDOWS\\Fonts\\KoPub Batang Light.ttf',
     'C:\\Windows\\Fonts\\NanumSquareRoundB.ttf',
     'C:\\WINDOWS\\Fonts\\simsunb.ttf',
     'C:\\WINDOWS\\Fonts\\GARABD.TTF',
     'C:\\Windows\\Fonts\\cour.ttf',
     'C:\\WINDOWS\\Fonts\\CENTURY.TTF',
     'C:\\WINDOWS\\Fonts\\나눔고딕코딩-Bold.ttf',
     'C:\\WINDOWS\\Fonts\\corbelb.ttf',
     'C:\\Windows\\Fonts\\corbeli.ttf',
     'C:\\WINDOWS\\Fonts\\sanssb__.ttf',
     'C:\\Windows\\Fonts\\CoureB.ttf',
     'C:\\WINDOWS\\Fonts\\H2GTRE.TTF',
     'C:\\WINDOWS\\Fonts\\SitkaI.ttc',
     'C:\\WINDOWS\\Fonts\\constan.ttf',
     'C:\\Windows\\Fonts\\monos.ttf',
     'C:\\WINDOWS\\Fonts\\seguisym.ttf',
     'C:\\WINDOWS\\Fonts\\swisscli.ttf',
     'C:\\Windows\\Fonts\\segoeuil.ttf',
     'C:\\Windows\\Fonts\\GOTHICI.TTF',
     'C:\\WINDOWS\\Fonts\\Inkfree.ttf',
     'C:\\WINDOWS\\Fonts\\AMDT_Symbols.ttf',
     'C:\\WINDOWS\\Fonts\\gadugib.ttf',
     'C:\\Windows\\Fonts\\BOOKOSBI.TTF',
     'C:\\WINDOWS\\Fonts\\palabi.ttf',
     'C:\\Windows\\Fonts\\swisscli.ttf',
     'C:\\WINDOWS\\Fonts\\H2SA1M.TTF',
     'C:\\WINDOWS\\Fonts\\WINGDNG2.TTF',
     'C:\\Windows\\Fonts\\H2GSRB.TTF',
     'C:\\WINDOWS\\Fonts\\BSSYM7.TTF',
     'C:\\Windows\\Fonts\\gadugi.ttf',
     'C:\\Windows\\Fonts\\counb___.ttf',
     'C:\\WINDOWS\\Fonts\\segoescb.ttf',
     'C:\\WINDOWS\\Fonts\\NirmalaS.ttf',
     'C:\\WINDOWS\\Fonts\\HanSantteutDotum-Regular.ttf',
     'C:\\Windows\\Fonts\\HANBatangB.ttf',
     'C:\\Windows\\Fonts\\YuGothB.ttc',
     'C:\\Windows\\Fonts\\cityb___.ttf',
     'C:\\WINDOWS\\Fonts\\italicc_.ttf',
     'C:\\WINDOWS\\Fonts\\OUTLOOK.TTF',
     'C:\\WINDOWS\\Fonts\\swissel.ttf',
     'C:\\WINDOWS\\Fonts\\symusic_.ttf',
     'C:\\Windows\\Fonts\\webdings.ttf',
     'C:\\Windows\\Fonts\\HANBatangExtB.ttf',
     'C:\\WINDOWS\\Fonts\\Sitka.ttc',
     'C:\\Windows\\Fonts\\DUBAI-BOLD.TTF',
     'C:\\Windows\\Fonts\\ariblk.ttf',
     'C:\\WINDOWS\\Fonts\\italict_.ttf',
     'C:\\Windows\\Fonts\\romai___.ttf',
     'C:\\WINDOWS\\Fonts\\LeelaUIb.ttf',
     'C:\\WINDOWS\\Fonts\\georgia.ttf',
     'C:\\WINDOWS\\Fonts\\GOTHICBI.TTF',
     'C:\\Windows\\Fonts\\monosb.ttf',
     'C:\\Windows\\Fonts\\corbell.ttf',
     'C:\\WINDOWS\\Fonts\\NanumSquareRoundL.ttf',
     'C:\\WINDOWS\\Fonts\\GOTHICI.TTF',
     'C:\\Windows\\Fonts\\seguili.ttf',
     'C:\\WINDOWS\\Fonts\\msyhbd.ttc',
     'C:\\Windows\\Fonts\\mtproxy4.ttf',
     'C:\\WINDOWS\\Fonts\\segoesc.ttf',
     'C:\\Windows\\Fonts\\Candaraz.ttf',
     'C:\\Windows\\Fonts\\comicz.ttf',
     'C:\\Windows\\Fonts\\l_10646.ttf',
     'C:\\Windows\\Fonts\\GARAIT.TTF',
     'C:\\Windows\\Fonts\\OUTLOOK.TTF',
     'C:\\WINDOWS\\Fonts\\cambriaz.ttf',
     'C:\\WINDOWS\\Fonts\\segoeui.ttf',
     'C:\\WINDOWS\\Fonts\\verdanaz.ttf',
     'C:\\WINDOWS\\Fonts\\gulim.ttc',
     'C:\\WINDOWS\\Fonts\\Nirmala.ttf',
     'C:\\Windows\\Fonts\\consolab.ttf',
     'C:\\Windows\\Fonts\\corbelli.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy2.ttf',
     'C:\\Windows\\Fonts\\trebucbi.ttf',
     'C:\\WINDOWS\\Fonts\\constanb.ttf',
     'C:\\Windows\\Fonts\\LeelawUI.ttf',
     'C:\\Windows\\Fonts\\supef___.ttf',
     'C:\\WINDOWS\\Fonts\\isocp___.ttf',
     'C:\\WINDOWS\\Fonts\\romai___.ttf',
     'C:\\Windows\\Fonts\\tahomabd.ttf',
     'C:\\Windows\\Fonts\\KoPub Batang Light.ttf',
     'C:\\Windows\\Fonts\\bahnschrift.ttf',
     'C:\\Windows\\Fonts\\swisscl.ttf',
     'C:\\WINDOWS\\Fonts\\calibrib.ttf',
     'C:\\WINDOWS\\Fonts\\H2GSRB.TTF',
     'C:\\Windows\\Fonts\\verdanab.ttf',
     'C:\\WINDOWS\\Fonts\\corbelli.ttf',
     'C:\\WINDOWS\\Fonts\\REFSAN.TTF',
     'C:\\WINDOWS\\Fonts\\mmrtextb.ttf',
     'C:\\Windows\\Fonts\\msyi.ttf',
     'C:\\WINDOWS\\Fonts\\HMFMPYUN.TTF',
     'C:\\WINDOWS\\Fonts\\segoeuisl.ttf',
     'C:\\WINDOWS\\Fonts\\seguibl.ttf',
     'C:\\Windows\\Fonts\\FiraCode-Retina.ttf',
     'C:\\Windows\\Fonts\\segoescb.ttf',
     'C:\\Windows\\Fonts\\AMDT_Symbols.ttf',
     'C:\\Windows\\Fonts\\consola.ttf',
     'C:\\Windows\\Fonts\\CoureBI.ttf',
     'C:\\WINDOWS\\Fonts\\swissko.ttf',
     'C:\\WINDOWS\\Fonts\\swissek.ttf',
     'C:\\WINDOWS\\Fonts\\calibrii.ttf',
     'C:\\Windows\\Fonts\\NanumSquareLight.ttf',
     'C:\\WINDOWS\\Fonts\\romab___.ttf',
     'C:\\WINDOWS\\Fonts\\arial.ttf',
     'C:\\Windows\\Fonts\\timesbd.ttf',
     'C:\\Windows\\Fonts\\seguisbi.ttf',
     'C:\\Windows\\Fonts\\mmrtextb.ttf',
     'C:\\WINDOWS\\Fonts\\cambria.ttc',
     'C:\\WINDOWS\\Fonts\\GARAIT.TTF',
     'C:\\WINDOWS\\Fonts\\isocpeur.ttf',
     'C:\\WINDOWS\\Fonts\\palai.ttf',
     'C:\\Windows\\Fonts\\swissk.ttf',
     'C:\\Windows\\Fonts\\Sitka.ttc',
     'C:\\WINDOWS\\Fonts\\H2PORM.TTF',
     'C:\\Windows\\Fonts\\trebuc.ttf',
     'C:\\Windows\\Fonts\\MTCORSVA.TTF',
     'C:\\Windows\\Fonts\\palabi.ttf',
     'C:\\Windows\\Fonts\\H2GPRM.TTF',
     'C:\\Windows\\Fonts\\complex_.ttf',
     'C:\\Windows\\Fonts\\georgiaz.ttf',
     'C:\\WINDOWS\\Fonts\\Candarab.ttf',
     'C:\\Windows\\Fonts\\ANTQUABI.TTF',
     'C:\\WINDOWS\\Fonts\\monos.ttf',
     'C:\\WINDOWS\\Fonts\\NanumGothicBold.ttf',
     'C:\\WINDOWS\\Fonts\\panroman.ttf',
     'C:\\Windows\\Fonts\\msyh.ttc',
     'C:\\Windows\\Fonts\\isocp2__.ttf',
     'C:\\WINDOWS\\Fonts\\monbaiti.ttf',
     'C:\\WINDOWS\\Fonts\\swisseb.ttf',
     'C:\\Windows\\Fonts\\ARIALNB.TTF',
     'C:\\Windows\\Fonts\\mtproxy2.ttf',
     'C:\\Windows\\Fonts\\GARA.TTF',
     'C:\\Windows\\Fonts\\taile.ttf',
     'C:\\Windows\\Fonts\\Nirmala.ttf',
     'C:\\WINDOWS\\Fonts\\greekc__.ttf',
     'C:\\Windows\\Fonts\\HMFMOLD.TTF',
     'C:\\WINDOWS\\Fonts\\timesi.ttf',
     'C:\\WINDOWS\\Fonts\\ariblk.ttf',
     'C:\\WINDOWS\\Fonts\\H2HDRM.TTF',
     'C:\\WINDOWS\\Fonts\\l_10646.ttf',
     'C:\\WINDOWS\\Fonts\\HANDotumB.ttf',
     'C:\\Windows\\Fonts\\DUBAI-LIGHT.TTF',
     'C:\\Windows\\Fonts\\calibril.ttf',
     'C:\\Windows\\Fonts\\swissko.ttf',
     'C:\\Windows\\Fonts\\romant__.ttf',
     'C:\\Windows\\Fonts\\courbd.ttf',
     'C:\\WINDOWS\\Fonts\\SymbP.ttf',
     'C:\\WINDOWS\\Fonts\\BOOKOS.TTF',
     'C:\\WINDOWS\\Fonts\\HMFMMUEX.TTC',
     'C:\\Windows\\Fonts\\calibriz.ttf',
     'C:\\Windows\\Fonts\\YuGothR.ttc',
     'C:\\WINDOWS\\Fonts\\HATTEN.TTF',
     'C:\\WINDOWS\\Fonts\\dutchb.ttf',
     'C:\\Windows\\Fonts\\swisseb.ttf',
     'C:\\Windows\\Fonts\\isocp___.ttf',
     'C:\\WINDOWS\\Fonts\\REFSPCL.TTF',
     'C:\\Windows\\Fonts\\HANBatangExtBB.ttf',
     'C:\\Windows\\Fonts\\BSSYM7.TTF',
     'C:\\WINDOWS\\Fonts\\NanumBarunpenBold.ttf',
     'C:\\WINDOWS\\Fonts\\monotxt_.ttf',
     'C:\\Windows\\Fonts\\NanumBrush.ttf',
     'C:\\WINDOWS\\Fonts\\gadugi.ttf',
     'C:\\Windows\\Fonts\\KoPub Dotum Medium.ttf',
     'C:\\WINDOWS\\Fonts\\dutch.ttf',
     'C:\\Windows\\Fonts\\vinet.ttf',
     'C:\\WINDOWS\\Fonts\\MTCORSVA.TTF',
     'C:\\WINDOWS\\Fonts\\NanumPen.ttf',
     'C:\\WINDOWS\\Fonts\\mmrtext.ttf',
     'C:\\WINDOWS\\Fonts\\mtproxy7.ttf',
     'C:\\Windows\\Fonts\\calibri.ttf',
     'C:\\Windows\\Fonts\\SymbC.ttf']




```python
import pandas as pd

# 각 글꼴 파일의 경로를 사용해서 정보객체 만들기
data_list = []
for v in flist:
    fprop = font_manager.FontProperties(fname=v)
    data_list.append({"file":fprop.get_file(), "name":fprop.get_name()})
    
df = pd.DataFrame(data_list)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>file</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>C:\Windows\Fonts\swisscbi.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>1</td>
      <td>C:\WINDOWS\Fonts\calibrili.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>2</td>
      <td>C:\Windows\Fonts\H2GTRM.TTF</td>
      <td>HYGothic-Medium</td>
    </tr>
    <tr>
      <td>3</td>
      <td>C:\WINDOWS\Fonts\isocp2__.ttf</td>
      <td>ISOCP2</td>
    </tr>
    <tr>
      <td>4</td>
      <td>C:\Windows\Fonts\gadugib.ttf</td>
      <td>Gadugi</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>724</td>
      <td>C:\WINDOWS\Fonts\NanumPen.ttf</td>
      <td>Nanum Pen Script</td>
    </tr>
    <tr>
      <td>725</td>
      <td>C:\WINDOWS\Fonts\mmrtext.ttf</td>
      <td>Myanmar Text</td>
    </tr>
    <tr>
      <td>726</td>
      <td>C:\WINDOWS\Fonts\mtproxy7.ttf</td>
      <td>Proxy 7</td>
    </tr>
    <tr>
      <td>727</td>
      <td>C:\Windows\Fonts\calibri.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>728</td>
      <td>C:\Windows\Fonts\SymbC.ttf</td>
      <td>CATIA Symbols</td>
    </tr>
  </tbody>
</table>
<p>729 rows × 2 columns</p>
</div>




```python
# 행 열의 수를 가져옴
행,열 = df.shape
print(행)
print(열)
```

    729
    2
    


```python
# pandas에게 표시할 최대 행 수를 전체 데이터 수로 설정하고 다시 출력함
pd.set_option('display.max_rows', 행)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>file</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>C:\Windows\Fonts\swisscbi.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>1</td>
      <td>C:\WINDOWS\Fonts\calibrili.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>2</td>
      <td>C:\Windows\Fonts\H2GTRM.TTF</td>
      <td>HYGothic-Medium</td>
    </tr>
    <tr>
      <td>3</td>
      <td>C:\WINDOWS\Fonts\isocp2__.ttf</td>
      <td>ISOCP2</td>
    </tr>
    <tr>
      <td>4</td>
      <td>C:\Windows\Fonts\gadugib.ttf</td>
      <td>Gadugi</td>
    </tr>
    <tr>
      <td>5</td>
      <td>C:\Windows\Fonts\H2HDRM.TTF</td>
      <td>HYHeadLine-Medium</td>
    </tr>
    <tr>
      <td>6</td>
      <td>C:\WINDOWS\Fonts\comicz.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>7</td>
      <td>C:\WINDOWS\Fonts\NirmalaB.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>8</td>
      <td>C:\Windows\Fonts\NanumPen.ttf</td>
      <td>Nanum Pen Script</td>
    </tr>
    <tr>
      <td>9</td>
      <td>C:\WINDOWS\Fonts\consolaz.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>10</td>
      <td>C:\WINDOWS\Fonts\pala.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>11</td>
      <td>C:\Windows\Fonts\Candara.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>12</td>
      <td>C:\WINDOWS\Fonts\Candara.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>13</td>
      <td>C:\WINDOWS\Fonts\swissck.ttf</td>
      <td>Swis721 BlkCn BT</td>
    </tr>
    <tr>
      <td>14</td>
      <td>C:\WINDOWS\Fonts\SymbM.ttf</td>
      <td>SymbolMono BT</td>
    </tr>
    <tr>
      <td>15</td>
      <td>C:\Windows\Fonts\segoeuii.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>16</td>
      <td>C:\WINDOWS\Fonts\verdanab.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>17</td>
      <td>C:\WINDOWS\Fonts\LeelUIsl.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>18</td>
      <td>C:\WINDOWS\Fonts\NanumSquareExtraBold.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>19</td>
      <td>C:\WINDOWS\Fonts\taile.ttf</td>
      <td>Microsoft Tai Le</td>
    </tr>
    <tr>
      <td>20</td>
      <td>C:\WINDOWS\Fonts\timesbi.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>21</td>
      <td>C:\Windows\Fonts\GENISO.ttf</td>
      <td>GENISO</td>
    </tr>
    <tr>
      <td>22</td>
      <td>C:\Windows\Fonts\HancomEQN.ttf</td>
      <td>HancomEQN</td>
    </tr>
    <tr>
      <td>23</td>
      <td>C:\WINDOWS\Fonts\swisscbi.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>24</td>
      <td>C:\WINDOWS\Fonts\ARIALNBI.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>25</td>
      <td>C:\WINDOWS\Fonts\msyh.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>26</td>
      <td>C:\Windows\Fonts\dutchi.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>27</td>
      <td>C:\Windows\Fonts\msyhl.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>28</td>
      <td>C:\WINDOWS\Fonts\seguisbi.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>29</td>
      <td>C:\WINDOWS\Fonts\couri.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>30</td>
      <td>C:\Windows\Fonts\BKANT.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>31</td>
      <td>C:\Windows\Fonts\mtproxy6.ttf</td>
      <td>Proxy 6</td>
    </tr>
    <tr>
      <td>32</td>
      <td>C:\Windows\Fonts\DUBAI-MEDIUM.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>33</td>
      <td>C:\Windows\Fonts\AIGDT___.TTF</td>
      <td>AIGDT</td>
    </tr>
    <tr>
      <td>34</td>
      <td>C:\Windows\Fonts\seguihis.ttf</td>
      <td>Segoe UI Historic</td>
    </tr>
    <tr>
      <td>35</td>
      <td>C:\Windows\Fonts\ariali.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>36</td>
      <td>C:\Windows\Fonts\cambriaz.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>37</td>
      <td>C:\WINDOWS\Fonts\ANTQUAI.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>38</td>
      <td>C:\Windows\Fonts\gothici_.ttf</td>
      <td>GothicI</td>
    </tr>
    <tr>
      <td>39</td>
      <td>C:\WINDOWS\Fonts\seguisb.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>40</td>
      <td>C:\WINDOWS\Fonts\constani.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>41</td>
      <td>C:\WINDOWS\Fonts\seguihis.ttf</td>
      <td>Segoe UI Historic</td>
    </tr>
    <tr>
      <td>42</td>
      <td>C:\Windows\Fonts\symap___.ttf</td>
      <td>Symap</td>
    </tr>
    <tr>
      <td>43</td>
      <td>C:\Windows\Fonts\NanumSquareExtraBold.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>44</td>
      <td>C:\Windows\Fonts\NanumSquareRoundEB.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>45</td>
      <td>C:\Windows\Fonts\GOTHICBI.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>46</td>
      <td>C:\WINDOWS\Fonts\AMGDT___.ttf</td>
      <td>AMGDT</td>
    </tr>
    <tr>
      <td>47</td>
      <td>C:\WINDOWS\Fonts\FiraCode-Retina.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>48</td>
      <td>C:\WINDOWS\Fonts\simplex_.ttf</td>
      <td>Simplex</td>
    </tr>
    <tr>
      <td>49</td>
      <td>C:\Windows\Fonts\HanSantteutDotumBold.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>50</td>
      <td>C:\Windows\Fonts\symath__.ttf</td>
      <td>Symath</td>
    </tr>
    <tr>
      <td>51</td>
      <td>C:\Windows\Fonts\segoeui.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>52</td>
      <td>C:\Windows\Fonts\syastro_.ttf</td>
      <td>Syastro</td>
    </tr>
    <tr>
      <td>53</td>
      <td>C:\Windows\Fonts\JUMJA.TTF</td>
      <td>NewJumja</td>
    </tr>
    <tr>
      <td>54</td>
      <td>C:\Windows\Fonts\stylu.ttf</td>
      <td>Stylus BT</td>
    </tr>
    <tr>
      <td>55</td>
      <td>C:\WINDOWS\Fonts\NGULIM.TTF</td>
      <td>New Gulim</td>
    </tr>
    <tr>
      <td>56</td>
      <td>C:\Windows\Fonts\micross.ttf</td>
      <td>Microsoft Sans Serif</td>
    </tr>
    <tr>
      <td>57</td>
      <td>C:\WINDOWS\Fonts\micross.ttf</td>
      <td>Microsoft Sans Serif</td>
    </tr>
    <tr>
      <td>58</td>
      <td>C:\Windows\Fonts\monbaiti.ttf</td>
      <td>Mongolian Baiti</td>
    </tr>
    <tr>
      <td>59</td>
      <td>C:\WINDOWS\Fonts\ebrima.ttf</td>
      <td>Ebrima</td>
    </tr>
    <tr>
      <td>60</td>
      <td>C:\Windows\Fonts\georgiai.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>61</td>
      <td>C:\Windows\Fonts\comici.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>62</td>
      <td>C:\WINDOWS\Fonts\D2CodingBold-Ver1.3-20171129.ttf</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>63</td>
      <td>C:\WINDOWS\Fonts\himalaya.ttf</td>
      <td>Microsoft Himalaya</td>
    </tr>
    <tr>
      <td>64</td>
      <td>C:\WINDOWS\Fonts\D2Coding-Ver1.3-20171129.ttf</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>65</td>
      <td>C:\WINDOWS\Fonts\BOOKOSBI.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>66</td>
      <td>C:\Windows\Fonts\couri.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>67</td>
      <td>C:\WINDOWS\Fonts\AcadEref.ttf</td>
      <td>AcadEref</td>
    </tr>
    <tr>
      <td>68</td>
      <td>C:\WINDOWS\Fonts\Candaral.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>69</td>
      <td>C:\WINDOWS\Fonts\isoct___.ttf</td>
      <td>ISOCT</td>
    </tr>
    <tr>
      <td>70</td>
      <td>C:\Windows\Fonts\swissli.ttf</td>
      <td>Swis721 Lt BT</td>
    </tr>
    <tr>
      <td>71</td>
      <td>C:\Windows\Fonts\swissci.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>72</td>
      <td>C:\WINDOWS\Fonts\DUBAI-REGULAR.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>73</td>
      <td>C:\WINDOWS\Fonts\NanumSquareBold.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>74</td>
      <td>C:\Windows\Fonts\techl___.ttf</td>
      <td>TechnicLite</td>
    </tr>
    <tr>
      <td>75</td>
      <td>C:\WINDOWS\Fonts\NanumGothic.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>76</td>
      <td>C:\Windows\Fonts\segoeuisl.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>77</td>
      <td>C:\Windows\Fonts\isocteui.ttf</td>
      <td>ISOCTEUR</td>
    </tr>
    <tr>
      <td>78</td>
      <td>C:\WINDOWS\Fonts\HanSantteutDotumRegular.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>79</td>
      <td>C:\Windows\Fonts\corbel.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>80</td>
      <td>C:\WINDOWS\Fonts\romand__.ttf</td>
      <td>RomanD</td>
    </tr>
    <tr>
      <td>81</td>
      <td>C:\Windows\Fonts\seguisym.ttf</td>
      <td>Segoe UI Symbol</td>
    </tr>
    <tr>
      <td>82</td>
      <td>C:\WINDOWS\Fonts\comicbd.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>83</td>
      <td>C:\Windows\Fonts\times.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>84</td>
      <td>C:\WINDOWS\Fonts\segoeuib.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>85</td>
      <td>C:\WINDOWS\Fonts\YuGothM.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>86</td>
      <td>C:\Windows\Fonts\Hancom Gothic Regular.ttf</td>
      <td>Hancom Gothic</td>
    </tr>
    <tr>
      <td>87</td>
      <td>C:\WINDOWS\Fonts\georgiaz.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>88</td>
      <td>C:\Windows\Fonts\REFSAN.TTF</td>
      <td>MS Reference Sans Serif</td>
    </tr>
    <tr>
      <td>89</td>
      <td>C:\Windows\Fonts\trebucit.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>90</td>
      <td>C:\WINDOWS\Fonts\YuGothR.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>91</td>
      <td>C:\Windows\Fonts\FiraCode-Light.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>92</td>
      <td>C:\WINDOWS\Fonts\monosb.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>93</td>
      <td>C:\WINDOWS\Fonts\ANTQUAB.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>94</td>
      <td>C:\WINDOWS\Fonts\DUBAI-BOLD.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>95</td>
      <td>C:\Windows\Fonts\NirmalaB.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>96</td>
      <td>C:\WINDOWS\Fonts\isocpeui.ttf</td>
      <td>ISOCPEUR</td>
    </tr>
    <tr>
      <td>97</td>
      <td>C:\WINDOWS\Fonts\swisscb.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>98</td>
      <td>C:\Windows\Fonts\H2PORL.TTF</td>
      <td>HYPost-Light</td>
    </tr>
    <tr>
      <td>99</td>
      <td>C:\WINDOWS\Fonts\verdanai.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>100</td>
      <td>C:\WINDOWS\Fonts\NanumBarunGothicLight.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>101</td>
      <td>C:\WINDOWS\Fonts\consolai.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>102</td>
      <td>C:\Windows\Fonts\eurro___.ttf</td>
      <td>EuroRoman</td>
    </tr>
    <tr>
      <td>103</td>
      <td>C:\Windows\Fonts\romab___.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>104</td>
      <td>C:\WINDOWS\Fonts\ntailu.ttf</td>
      <td>Microsoft New Tai Lue</td>
    </tr>
    <tr>
      <td>105</td>
      <td>C:\WINDOWS\Fonts\swissli.ttf</td>
      <td>Swis721 Lt BT</td>
    </tr>
    <tr>
      <td>106</td>
      <td>C:\Windows\Fonts\romans__.ttf</td>
      <td>RomanS</td>
    </tr>
    <tr>
      <td>107</td>
      <td>C:\Windows\Fonts\swisscki.ttf</td>
      <td>Swis721 BlkCn BT</td>
    </tr>
    <tr>
      <td>108</td>
      <td>C:\WINDOWS\Fonts\NanumSquareRoundR.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>109</td>
      <td>C:\WINDOWS\Fonts\isoct2__.ttf</td>
      <td>ISOCT2</td>
    </tr>
    <tr>
      <td>110</td>
      <td>C:\WINDOWS\Fonts\YuGothL.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>111</td>
      <td>C:\Windows\Fonts\swisscb.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>112</td>
      <td>C:\Windows\Fonts\malgunbd_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>113</td>
      <td>C:\Windows\Fonts\holomdl2.ttf</td>
      <td>HoloLens MDL2 Assets</td>
    </tr>
    <tr>
      <td>114</td>
      <td>C:\WINDOWS\Fonts\palab.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>115</td>
      <td>C:\WINDOWS\Fonts\HancomEQN.ttf</td>
      <td>HancomEQN</td>
    </tr>
    <tr>
      <td>116</td>
      <td>C:\Windows\Fonts\HANBatangExt.ttf</td>
      <td>HCR Batang Ext</td>
    </tr>
    <tr>
      <td>117</td>
      <td>C:\Windows\Fonts\greekc__.ttf</td>
      <td>GreekC</td>
    </tr>
    <tr>
      <td>118</td>
      <td>C:\WINDOWS\Fonts\eurro___.ttf</td>
      <td>EuroRoman</td>
    </tr>
    <tr>
      <td>119</td>
      <td>C:\WINDOWS\Fonts\syastro_.ttf</td>
      <td>Syastro</td>
    </tr>
    <tr>
      <td>120</td>
      <td>C:\WINDOWS\Fonts\GOTHICB.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>121</td>
      <td>C:\WINDOWS\Fonts\HanSantteutDotum-Bold.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>122</td>
      <td>C:\Windows\Fonts\isocteur.ttf</td>
      <td>ISOCTEUR</td>
    </tr>
    <tr>
      <td>123</td>
      <td>C:\Windows\Fonts\Candarai.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>124</td>
      <td>C:\Windows\Fonts\tahoma.ttf</td>
      <td>Tahoma</td>
    </tr>
    <tr>
      <td>125</td>
      <td>C:\WINDOWS\Fonts\BOOKOSB.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>126</td>
      <td>C:\WINDOWS\Fonts\trebucbi.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>127</td>
      <td>C:\WINDOWS\Fonts\romanc__.ttf</td>
      <td>RomanC</td>
    </tr>
    <tr>
      <td>128</td>
      <td>C:\Windows\Fonts\arial.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>129</td>
      <td>C:\Windows\Fonts\GARABD.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>130</td>
      <td>C:\WINDOWS\Fonts\impact.ttf</td>
      <td>Impact</td>
    </tr>
    <tr>
      <td>131</td>
      <td>C:\Windows\Fonts\monotxt_.ttf</td>
      <td>Monotxt</td>
    </tr>
    <tr>
      <td>132</td>
      <td>C:\Windows\Fonts\constanz.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>133</td>
      <td>C:\Windows\Fonts\WINGDNG2.TTF</td>
      <td>Wingdings 2</td>
    </tr>
    <tr>
      <td>134</td>
      <td>C:\WINDOWS\Fonts\arialbi.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>135</td>
      <td>C:\WINDOWS\Fonts\D2Coding-Ver1.3-20171129.ttc</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>136</td>
      <td>C:\WINDOWS\Fonts\FiraCode-Regular.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>137</td>
      <td>C:\Windows\Fonts\consolai.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>138</td>
      <td>C:\Windows\Fonts\HANDotum.ttf</td>
      <td>HCR Dotum</td>
    </tr>
    <tr>
      <td>139</td>
      <td>C:\Windows\Fonts\cambriai.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>140</td>
      <td>C:\WINDOWS\Fonts\NanumBrush.ttf</td>
      <td>Nanum Brush Script</td>
    </tr>
    <tr>
      <td>141</td>
      <td>C:\WINDOWS\Fonts\KoPub Dotum Light.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>142</td>
      <td>C:\WINDOWS\Fonts\calibriz.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>143</td>
      <td>C:\Windows\Fonts\taileb.ttf</td>
      <td>Microsoft Tai Le</td>
    </tr>
    <tr>
      <td>144</td>
      <td>C:\Windows\Fonts\NanumSquareRegular.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>145</td>
      <td>C:\Windows\Fonts\palai.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>146</td>
      <td>C:\Windows\Fonts\simsunb.ttf</td>
      <td>SimSun-ExtB</td>
    </tr>
    <tr>
      <td>147</td>
      <td>C:\Windows\Fonts\techb___.ttf</td>
      <td>TechnicBold</td>
    </tr>
    <tr>
      <td>148</td>
      <td>C:\WINDOWS\Fonts\bgothm.ttf</td>
      <td>BankGothic Md BT</td>
    </tr>
    <tr>
      <td>149</td>
      <td>C:\Windows\Fonts\mtproxy1.ttf</td>
      <td>Proxy 1</td>
    </tr>
    <tr>
      <td>150</td>
      <td>C:\Windows\Fonts\BOOKOSB.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>151</td>
      <td>C:\Windows\Fonts\Candarali.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>152</td>
      <td>C:\Windows\Fonts\swiss.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>153</td>
      <td>C:\WINDOWS\Fonts\CoureI.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>154</td>
      <td>C:\WINDOWS\Fonts\NanumMyeongjoExtraBold.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>155</td>
      <td>C:\Windows\Fonts\isocpeur.ttf</td>
      <td>ISOCPEUR</td>
    </tr>
    <tr>
      <td>156</td>
      <td>C:\Windows\Fonts\LeelUIsl.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>157</td>
      <td>C:\Windows\Fonts\ebrima.ttf</td>
      <td>Ebrima</td>
    </tr>
    <tr>
      <td>158</td>
      <td>C:\WINDOWS\Fonts\techl___.ttf</td>
      <td>TechnicLite</td>
    </tr>
    <tr>
      <td>159</td>
      <td>C:\WINDOWS\Fonts\ariali.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>160</td>
      <td>C:\WINDOWS\Fonts\BOOKOSI.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>161</td>
      <td>C:\WINDOWS\Fonts\msjhl.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>162</td>
      <td>C:\Windows\Fonts\WINGDNG3.TTF</td>
      <td>Wingdings 3</td>
    </tr>
    <tr>
      <td>163</td>
      <td>C:\WINDOWS\Fonts\swissc.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>164</td>
      <td>C:\Windows\Fonts\DUBAI-REGULAR.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>165</td>
      <td>C:\Windows\Fonts\H2MKPB.TTF</td>
      <td>HYPMokGak-Bold</td>
    </tr>
    <tr>
      <td>166</td>
      <td>C:\Windows\Fonts\malgunsl_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>167</td>
      <td>C:\Windows\Fonts\calibrii.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>168</td>
      <td>C:\Windows\Fonts\greeks__.ttf</td>
      <td>GreekS</td>
    </tr>
    <tr>
      <td>169</td>
      <td>C:\Windows\Fonts\HANBatang.ttf</td>
      <td>HCR Batang</td>
    </tr>
    <tr>
      <td>170</td>
      <td>C:\Windows\Fonts\swissi.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>171</td>
      <td>C:\Windows\Fonts\NanumMyeongjoExtraBold.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>172</td>
      <td>C:\Windows\Fonts\SymbP.ttf</td>
      <td>SymbolProp BT</td>
    </tr>
    <tr>
      <td>173</td>
      <td>C:\WINDOWS\Fonts\cityb___.ttf</td>
      <td>CityBlueprint</td>
    </tr>
    <tr>
      <td>174</td>
      <td>C:\WINDOWS\Fonts\swiss.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>175</td>
      <td>C:\Windows\Fonts\GOTHIC.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>176</td>
      <td>C:\Windows\Fonts\cambria.ttc</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>177</td>
      <td>C:\WINDOWS\Fonts\mtproxy8.ttf</td>
      <td>Proxy 8</td>
    </tr>
    <tr>
      <td>178</td>
      <td>C:\Windows\Fonts\italicc_.ttf</td>
      <td>ItalicC</td>
    </tr>
    <tr>
      <td>179</td>
      <td>C:\WINDOWS\Fonts\AIGDT___.TTF</td>
      <td>AIGDT</td>
    </tr>
    <tr>
      <td>180</td>
      <td>C:\WINDOWS\Fonts\swissb.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>181</td>
      <td>C:\WINDOWS\Fonts\swisscbo.ttf</td>
      <td>Swis721 BdCnOul BT</td>
    </tr>
    <tr>
      <td>182</td>
      <td>C:\WINDOWS\Fonts\wingding.ttf</td>
      <td>Wingdings</td>
    </tr>
    <tr>
      <td>183</td>
      <td>C:\Windows\Fonts\NanumMyeongjo.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>184</td>
      <td>C:\Windows\Fonts\swisscbo.ttf</td>
      <td>Swis721 BdCnOul BT</td>
    </tr>
    <tr>
      <td>185</td>
      <td>C:\WINDOWS\Fonts\dutchbi.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>186</td>
      <td>C:\WINDOWS\Fonts\gdt_____.ttf</td>
      <td>GDT</td>
    </tr>
    <tr>
      <td>187</td>
      <td>C:\WINDOWS\Fonts\bgothl.ttf</td>
      <td>BankGothic Lt BT</td>
    </tr>
    <tr>
      <td>188</td>
      <td>C:\Windows\Fonts\verdanai.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>189</td>
      <td>C:\Windows\Fonts\NanumBarunGothicUltraLight.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>190</td>
      <td>C:\WINDOWS\Fonts\comsc.ttf</td>
      <td>CommercialScript BT</td>
    </tr>
    <tr>
      <td>191</td>
      <td>C:\Windows\Fonts\mingliub.ttc</td>
      <td>MingLiU-ExtB</td>
    </tr>
    <tr>
      <td>192</td>
      <td>C:\WINDOWS\Fonts\GARA.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>193</td>
      <td>C:\WINDOWS\Fonts\HANDotum.ttf</td>
      <td>HCR Dotum</td>
    </tr>
    <tr>
      <td>194</td>
      <td>C:\Windows\Fonts\REFSPCL.TTF</td>
      <td>MS Reference Specialty</td>
    </tr>
    <tr>
      <td>195</td>
      <td>C:\Windows\Fonts\sanssbo_.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>196</td>
      <td>C:\WINDOWS\Fonts\mtproxy6.ttf</td>
      <td>Proxy 6</td>
    </tr>
    <tr>
      <td>197</td>
      <td>C:\Windows\Fonts\dutchbi.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>198</td>
      <td>C:\Windows\Fonts\romanc__.ttf</td>
      <td>RomanC</td>
    </tr>
    <tr>
      <td>199</td>
      <td>C:\WINDOWS\Fonts\H2MJRE.TTF</td>
      <td>HYMyeongJo-Extra</td>
    </tr>
    <tr>
      <td>200</td>
      <td>C:\Windows\Fonts\verdana.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>201</td>
      <td>C:\WINDOWS\Fonts\swissbo.ttf</td>
      <td>Swis721 BdOul BT</td>
    </tr>
    <tr>
      <td>202</td>
      <td>C:\Windows\Fonts\NanumGothicBold.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>203</td>
      <td>C:\WINDOWS\Fonts\BKANT.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>204</td>
      <td>C:\WINDOWS\Fonts\courbd.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>205</td>
      <td>C:\WINDOWS\Fonts\isocteur.ttf</td>
      <td>ISOCTEUR</td>
    </tr>
    <tr>
      <td>206</td>
      <td>C:\Windows\Fonts\italic__.ttf</td>
      <td>Italic</td>
    </tr>
    <tr>
      <td>207</td>
      <td>C:\WINDOWS\Fonts\FiraCode-Medium.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>208</td>
      <td>C:\Windows\Fonts\georgia.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>209</td>
      <td>C:\WINDOWS\Fonts\WINGDNG3.TTF</td>
      <td>Wingdings 3</td>
    </tr>
    <tr>
      <td>210</td>
      <td>C:\WINDOWS\Fonts\NanumBarunpenRegular.ttf</td>
      <td>NanumBarunpen</td>
    </tr>
    <tr>
      <td>211</td>
      <td>C:\WINDOWS\Fonts\holomdl2.ttf</td>
      <td>HoloLens MDL2 Assets</td>
    </tr>
    <tr>
      <td>212</td>
      <td>C:\Windows\Fonts\isoct___.ttf</td>
      <td>ISOCT</td>
    </tr>
    <tr>
      <td>213</td>
      <td>C:\WINDOWS\Fonts\NanumGothicExtraBold.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>214</td>
      <td>C:\WINDOWS\Fonts\batang.ttc</td>
      <td>Batang</td>
    </tr>
    <tr>
      <td>215</td>
      <td>C:\WINDOWS\Fonts\romantic.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>216</td>
      <td>C:\Windows\Fonts\SitkaZ.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>217</td>
      <td>C:\WINDOWS\Fonts\msgothic.ttc</td>
      <td>MS Gothic</td>
    </tr>
    <tr>
      <td>218</td>
      <td>C:\Windows\Fonts\NanumBarunpenBold.ttf</td>
      <td>NanumBarunpen</td>
    </tr>
    <tr>
      <td>219</td>
      <td>C:\WINDOWS\Fonts\Candaraz.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>220</td>
      <td>C:\WINDOWS\Fonts\dutcheb.ttf</td>
      <td>Dutch801 XBd BT</td>
    </tr>
    <tr>
      <td>221</td>
      <td>C:\WINDOWS\Fonts\vinet.ttf</td>
      <td>Vineta BT</td>
    </tr>
    <tr>
      <td>222</td>
      <td>C:\Windows\Fonts\swissc.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>223</td>
      <td>C:\Windows\Fonts\NanumGothicLight.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>224</td>
      <td>C:\WINDOWS\Fonts\Hancom Gothic Regular.ttf</td>
      <td>Hancom Gothic</td>
    </tr>
    <tr>
      <td>225</td>
      <td>C:\Windows\Fonts\umath.ttf</td>
      <td>UniversalMath1 BT</td>
    </tr>
    <tr>
      <td>226</td>
      <td>C:\WINDOWS\Fonts\supef___.ttf</td>
      <td>SuperFrench</td>
    </tr>
    <tr>
      <td>227</td>
      <td>C:\Windows\Fonts\AMGDT___.ttf</td>
      <td>AMGDT</td>
    </tr>
    <tr>
      <td>228</td>
      <td>C:\Windows\Fonts\NanumBarunGothicBold.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>229</td>
      <td>C:\Windows\Fonts\segoesc.ttf</td>
      <td>Segoe Script</td>
    </tr>
    <tr>
      <td>230</td>
      <td>C:\WINDOWS\Fonts\trebucit.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>231</td>
      <td>C:\WINDOWS\Fonts\ARIALNI.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>232</td>
      <td>C:\WINDOWS\Fonts\malgunsl.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>233</td>
      <td>C:\WINDOWS\Fonts\swissk.ttf</td>
      <td>Swis721 Blk BT</td>
    </tr>
    <tr>
      <td>234</td>
      <td>C:\WINDOWS\Fonts\swissci.ttf</td>
      <td>Swis721 Cn BT</td>
    </tr>
    <tr>
      <td>235</td>
      <td>C:\WINDOWS\Fonts\stylu.ttf</td>
      <td>Stylus BT</td>
    </tr>
    <tr>
      <td>236</td>
      <td>C:\Windows\Fonts\NirmalaS.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>237</td>
      <td>C:\WINDOWS\Fonts\malgunbd.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>238</td>
      <td>C:\WINDOWS\Fonts\NanumMyeongjo.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>239</td>
      <td>C:\WINDOWS\Fonts\LeelawUI.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>240</td>
      <td>C:\WINDOWS\Fonts\CoureBI.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>241</td>
      <td>C:\WINDOWS\Fonts\H2PORL.TTF</td>
      <td>HYPost-Light</td>
    </tr>
    <tr>
      <td>242</td>
      <td>C:\WINDOWS\Fonts\georgiai.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>243</td>
      <td>C:\WINDOWS\Fonts\Candarali.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>244</td>
      <td>C:\WINDOWS\Fonts\KoPub Dotum Bold.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>245</td>
      <td>C:\WINDOWS\Fonts\HANBatangExt.ttf</td>
      <td>HCR Batang Ext</td>
    </tr>
    <tr>
      <td>246</td>
      <td>C:\Windows\Fonts\consolaz.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>247</td>
      <td>C:\WINDOWS\Fonts\seguiemj.ttf</td>
      <td>Segoe UI Emoji</td>
    </tr>
    <tr>
      <td>248</td>
      <td>C:\WINDOWS\Fonts\cambriai.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>249</td>
      <td>C:\WINDOWS\Fonts\phagspa.ttf</td>
      <td>Microsoft PhagsPa</td>
    </tr>
    <tr>
      <td>250</td>
      <td>C:\Windows\Fonts\mtproxy3.ttf</td>
      <td>Proxy 3</td>
    </tr>
    <tr>
      <td>251</td>
      <td>C:\WINDOWS\Fonts\CoureB.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>252</td>
      <td>C:\Windows\Fonts\HATTEN.TTF</td>
      <td>Haettenschweiler</td>
    </tr>
    <tr>
      <td>253</td>
      <td>C:\Windows\Fonts\seguibl.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>254</td>
      <td>C:\WINDOWS\Fonts\HMFMOLD.TTF</td>
      <td>Yet R</td>
    </tr>
    <tr>
      <td>255</td>
      <td>C:\Windows\Fonts\mtproxy9.ttf</td>
      <td>Proxy 9</td>
    </tr>
    <tr>
      <td>256</td>
      <td>C:\WINDOWS\Fonts\NanumBarunGothicUltraLight.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>257</td>
      <td>C:\Windows\Fonts\NanumMyeongjoBold.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>258</td>
      <td>C:\WINDOWS\Fonts\corbel.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>259</td>
      <td>C:\WINDOWS\Fonts\mtproxy9.ttf</td>
      <td>Proxy 9</td>
    </tr>
    <tr>
      <td>260</td>
      <td>C:\Windows\Fonts\HMKMRHD.TTF</td>
      <td>Headline R</td>
    </tr>
    <tr>
      <td>261</td>
      <td>C:\Windows\Fonts\malgunbd.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>262</td>
      <td>C:\Windows\Fonts\NanumSquareRoundR.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>263</td>
      <td>C:\WINDOWS\Fonts\NanumSquareLight.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>264</td>
      <td>C:\WINDOWS\Fonts\segmdl2.ttf</td>
      <td>Segoe MDL2 Assets</td>
    </tr>
    <tr>
      <td>265</td>
      <td>C:\WINDOWS\Fonts\corbell.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>266</td>
      <td>C:\WINDOWS\Fonts\HANBatangB.ttf</td>
      <td>HCR Batang</td>
    </tr>
    <tr>
      <td>267</td>
      <td>C:\WINDOWS\Fonts\consolab.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>268</td>
      <td>C:\Windows\Fonts\BOOKOSI.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>269</td>
      <td>C:\Windows\Fonts\Inkfree.ttf</td>
      <td>Ink Free</td>
    </tr>
    <tr>
      <td>270</td>
      <td>C:\WINDOWS\Fonts\SitkaZ.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>271</td>
      <td>C:\WINDOWS\Fonts\dutchi.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>272</td>
      <td>C:\Windows\Fonts\framdit.ttf</td>
      <td>Franklin Gothic Medium</td>
    </tr>
    <tr>
      <td>273</td>
      <td>C:\WINDOWS\Fonts\malgun_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>274</td>
      <td>C:\WINDOWS\Fonts\bahnschrift.ttf</td>
      <td>Bahnschrift</td>
    </tr>
    <tr>
      <td>275</td>
      <td>C:\WINDOWS\Fonts\verdana.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>276</td>
      <td>C:\Windows\Fonts\CoureI.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>277</td>
      <td>C:\Windows\Fonts\seguisli.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>278</td>
      <td>C:\WINDOWS\Fonts\ntailub.ttf</td>
      <td>Microsoft New Tai Lue</td>
    </tr>
    <tr>
      <td>279</td>
      <td>C:\Windows\Fonts\swissb.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>280</td>
      <td>C:\Windows\Fonts\ntailub.ttf</td>
      <td>Microsoft New Tai Lue</td>
    </tr>
    <tr>
      <td>281</td>
      <td>C:\Windows\Fonts\ARIALNBI.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>282</td>
      <td>C:\Windows\Fonts\NanumBarunGothicLight.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>283</td>
      <td>C:\Windows\Fonts\NanumGothic.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>284</td>
      <td>C:\Windows\Fonts\arialbd.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>285</td>
      <td>C:\Windows\Fonts\malgunsl.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>286</td>
      <td>C:\WINDOWS\Fonts\HYHWPEQ.TTF</td>
      <td>HyhwpEQ</td>
    </tr>
    <tr>
      <td>287</td>
      <td>C:\Windows\Fonts\BOOKOS.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>288</td>
      <td>C:\Windows\Fonts\monosbi.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>289</td>
      <td>C:\Windows\Fonts\sanss___.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>290</td>
      <td>C:\Windows\Fonts\verdanaz.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>291</td>
      <td>C:\Windows\Fonts\comsc.ttf</td>
      <td>CommercialScript BT</td>
    </tr>
    <tr>
      <td>292</td>
      <td>C:\WINDOWS\Fonts\segoeprb.ttf</td>
      <td>Segoe Print</td>
    </tr>
    <tr>
      <td>293</td>
      <td>C:\WINDOWS\Fonts\SymbC.ttf</td>
      <td>CATIA Symbols</td>
    </tr>
    <tr>
      <td>294</td>
      <td>C:\WINDOWS\Fonts\HMKMRHD.TTF</td>
      <td>Headline R</td>
    </tr>
    <tr>
      <td>295</td>
      <td>C:\Windows\Fonts\H2MJSM.TTF</td>
      <td>HYSinMyeongJo-Medium</td>
    </tr>
    <tr>
      <td>296</td>
      <td>C:\WINDOWS\Fonts\NanumSquareRoundEB.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>297</td>
      <td>C:\Windows\Fonts\NanumBarunGothic.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>298</td>
      <td>C:\WINDOWS\Fonts\swisscl.ttf</td>
      <td>Swis721 LtCn BT</td>
    </tr>
    <tr>
      <td>299</td>
      <td>C:\Windows\Fonts\courbi.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>300</td>
      <td>C:\WINDOWS\Fonts\sanssbo_.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>301</td>
      <td>C:\Windows\Fonts\FiraCode-Medium.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>302</td>
      <td>C:\WINDOWS\Fonts\HANWing2.ttf</td>
      <td>Haan Wing2</td>
    </tr>
    <tr>
      <td>303</td>
      <td>C:\WINDOWS\Fonts\seguisli.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>304</td>
      <td>C:\WINDOWS\Fonts\monosi.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>305</td>
      <td>C:\Windows\Fonts\HMKMMAG.TTF</td>
      <td>Magic R</td>
    </tr>
    <tr>
      <td>306</td>
      <td>C:\Windows\Fonts\segoepr.ttf</td>
      <td>Segoe Print</td>
    </tr>
    <tr>
      <td>307</td>
      <td>C:\Windows\Fonts\eurr____.ttf</td>
      <td>EuroRoman</td>
    </tr>
    <tr>
      <td>308</td>
      <td>C:\Windows\Fonts\simplex_.ttf</td>
      <td>Simplex</td>
    </tr>
    <tr>
      <td>309</td>
      <td>C:\WINDOWS\Fonts\isocp3__.ttf</td>
      <td>ISOCP3</td>
    </tr>
    <tr>
      <td>310</td>
      <td>C:\Windows\Fonts\D2CodingBold-Ver1.3-20171129.ttf</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>311</td>
      <td>C:\WINDOWS\Fonts\times.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>312</td>
      <td>C:\Windows\Fonts\isocp3__.ttf</td>
      <td>ISOCP3</td>
    </tr>
    <tr>
      <td>313</td>
      <td>C:\Windows\Fonts\NGULIM.TTF</td>
      <td>New Gulim</td>
    </tr>
    <tr>
      <td>314</td>
      <td>C:\Windows\Fonts\georgiab.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>315</td>
      <td>C:\WINDOWS\Fonts\eurr____.ttf</td>
      <td>EuroRoman</td>
    </tr>
    <tr>
      <td>316</td>
      <td>C:\Windows\Fonts\HMFMMUEX.TTC</td>
      <td>MoeumT R</td>
    </tr>
    <tr>
      <td>317</td>
      <td>C:\WINDOWS\Fonts\greeks__.ttf</td>
      <td>GreekS</td>
    </tr>
    <tr>
      <td>318</td>
      <td>C:\WINDOWS\Fonts\romans__.ttf</td>
      <td>RomanS</td>
    </tr>
    <tr>
      <td>319</td>
      <td>C:\Windows\Fonts\Gabriola.ttf</td>
      <td>Gabriola</td>
    </tr>
    <tr>
      <td>320</td>
      <td>C:\Windows\Fonts\NanumSquareRoundL.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>321</td>
      <td>C:\WINDOWS\Fonts\framd.ttf</td>
      <td>Franklin Gothic Medium</td>
    </tr>
    <tr>
      <td>322</td>
      <td>C:\Windows\Fonts\gothicg_.ttf</td>
      <td>GothicG</td>
    </tr>
    <tr>
      <td>323</td>
      <td>C:\Windows\Fonts\ARIALNI.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>324</td>
      <td>C:\WINDOWS\Fonts\mingliub.ttc</td>
      <td>MingLiU-ExtB</td>
    </tr>
    <tr>
      <td>325</td>
      <td>C:\WINDOWS\Fonts\JUMJA.TTF</td>
      <td>NewJumja</td>
    </tr>
    <tr>
      <td>326</td>
      <td>C:\WINDOWS\Fonts\malgun.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>327</td>
      <td>C:\Windows\Fonts\나눔고딕코딩.ttf</td>
      <td>NanumGothicCoding</td>
    </tr>
    <tr>
      <td>328</td>
      <td>C:\Windows\Fonts\trebucbd.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>329</td>
      <td>C:\Windows\Fonts\isoct3__.ttf</td>
      <td>ISOCT3</td>
    </tr>
    <tr>
      <td>330</td>
      <td>C:\Windows\Fonts\dutcheb.ttf</td>
      <td>Dutch801 XBd BT</td>
    </tr>
    <tr>
      <td>331</td>
      <td>C:\Windows\Fonts\romand__.ttf</td>
      <td>RomanD</td>
    </tr>
    <tr>
      <td>332</td>
      <td>C:\WINDOWS\Fonts\HANBatangExtB.ttf</td>
      <td>HCR Batang ExtB</td>
    </tr>
    <tr>
      <td>333</td>
      <td>C:\WINDOWS\Fonts\msjh.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>334</td>
      <td>C:\Windows\Fonts\himalaya.ttf</td>
      <td>Microsoft Himalaya</td>
    </tr>
    <tr>
      <td>335</td>
      <td>C:\Windows\Fonts\segmdl2.ttf</td>
      <td>Segoe MDL2 Assets</td>
    </tr>
    <tr>
      <td>336</td>
      <td>C:\Windows\Fonts\bgothm.ttf</td>
      <td>BankGothic Md BT</td>
    </tr>
    <tr>
      <td>337</td>
      <td>C:\WINDOWS\Fonts\simsun.ttc</td>
      <td>SimSun</td>
    </tr>
    <tr>
      <td>338</td>
      <td>C:\WINDOWS\Fonts\javatext.ttf</td>
      <td>Javanese Text</td>
    </tr>
    <tr>
      <td>339</td>
      <td>C:\WINDOWS\Fonts\counb___.ttf</td>
      <td>CountryBlueprint</td>
    </tr>
    <tr>
      <td>340</td>
      <td>C:\Windows\Fonts\D2Coding-Ver1.3-20171129.ttc</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>341</td>
      <td>C:\Windows\Fonts\scriptc_.ttf</td>
      <td>ScriptC</td>
    </tr>
    <tr>
      <td>342</td>
      <td>C:\WINDOWS\Fonts\calibril.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>343</td>
      <td>C:\Windows\Fonts\wingding.ttf</td>
      <td>Wingdings</td>
    </tr>
    <tr>
      <td>344</td>
      <td>C:\Windows\Fonts\FiraCode-Bold.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>345</td>
      <td>C:\Windows\Fonts\constan.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>346</td>
      <td>C:\Windows\Fonts\isoct2__.ttf</td>
      <td>ISOCT2</td>
    </tr>
    <tr>
      <td>347</td>
      <td>C:\WINDOWS\Fonts\phagspab.ttf</td>
      <td>Microsoft PhagsPa</td>
    </tr>
    <tr>
      <td>348</td>
      <td>C:\WINDOWS\Fonts\scripts_.ttf</td>
      <td>ScriptS</td>
    </tr>
    <tr>
      <td>349</td>
      <td>C:\Windows\Fonts\H2GTRE.TTF</td>
      <td>HYGothic-Extra</td>
    </tr>
    <tr>
      <td>350</td>
      <td>C:\WINDOWS\Fonts\NanumGothicLight.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>351</td>
      <td>C:\Windows\Fonts\KoPub Batang Medium.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>352</td>
      <td>C:\Windows\Fonts\italict_.ttf</td>
      <td>ItalicT</td>
    </tr>
    <tr>
      <td>353</td>
      <td>C:\WINDOWS\Fonts\YuGothB.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>354</td>
      <td>C:\Windows\Fonts\HanSantteutDotumRegular.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>355</td>
      <td>C:\Windows\Fonts\batang.ttc</td>
      <td>Batang</td>
    </tr>
    <tr>
      <td>356</td>
      <td>C:\WINDOWS\Fonts\cambriab.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>357</td>
      <td>C:\Windows\Fonts\msjhbd.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>358</td>
      <td>C:\WINDOWS\Fonts\comic.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>359</td>
      <td>C:\WINDOWS\Fonts\corbelz.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>360</td>
      <td>C:\Windows\Fonts\segoeuib.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>361</td>
      <td>C:\Windows\Fonts\malgun_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>362</td>
      <td>C:\WINDOWS\Fonts\seguibli.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>363</td>
      <td>C:\WINDOWS\Fonts\italic__.ttf</td>
      <td>Italic</td>
    </tr>
    <tr>
      <td>364</td>
      <td>C:\WINDOWS\Fonts\mvboli.ttf</td>
      <td>MV Boli</td>
    </tr>
    <tr>
      <td>365</td>
      <td>C:\Windows\Fonts\H2MJRE.TTF</td>
      <td>HYMyeongJo-Extra</td>
    </tr>
    <tr>
      <td>366</td>
      <td>C:\Windows\Fonts\gulim.ttc</td>
      <td>Gulim</td>
    </tr>
    <tr>
      <td>367</td>
      <td>C:\WINDOWS\Fonts\HANBatangExtBB.ttf</td>
      <td>HCR Batang ExtB</td>
    </tr>
    <tr>
      <td>368</td>
      <td>C:\WINDOWS\Fonts\seguili.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>369</td>
      <td>C:\Windows\Fonts\msgothic.ttc</td>
      <td>MS Gothic</td>
    </tr>
    <tr>
      <td>370</td>
      <td>C:\Windows\Fonts\pala.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>371</td>
      <td>C:\WINDOWS\Fonts\comici.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>372</td>
      <td>C:\WINDOWS\Fonts\webdings.ttf</td>
      <td>Webdings</td>
    </tr>
    <tr>
      <td>373</td>
      <td>C:\WINDOWS\Fonts\symeteo_.ttf</td>
      <td>Symeteo</td>
    </tr>
    <tr>
      <td>374</td>
      <td>C:\Windows\Fonts\swissek.ttf</td>
      <td>Swis721 BlkEx BT</td>
    </tr>
    <tr>
      <td>375</td>
      <td>C:\WINDOWS\Fonts\NanumSquareRegular.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>376</td>
      <td>C:\Windows\Fonts\monosi.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>377</td>
      <td>C:\Windows\Fonts\HANWing2.ttf</td>
      <td>Haan Wing2</td>
    </tr>
    <tr>
      <td>378</td>
      <td>C:\WINDOWS\Fonts\sansso__.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>379</td>
      <td>C:\Windows\Fonts\seguiemj.ttf</td>
      <td>Segoe UI Emoji</td>
    </tr>
    <tr>
      <td>380</td>
      <td>C:\WINDOWS\Fonts\gothici_.ttf</td>
      <td>GothicI</td>
    </tr>
    <tr>
      <td>381</td>
      <td>C:\Windows\Fonts\NanumGothicExtraBold.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>382</td>
      <td>C:\WINDOWS\Fonts\msyhl.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>383</td>
      <td>C:\Windows\Fonts\palab.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>384</td>
      <td>C:\Windows\Fonts\ANTQUAI.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>385</td>
      <td>C:\WINDOWS\Fonts\calibri.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>386</td>
      <td>C:\WINDOWS\Fonts\KoPub Dotum Medium.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>387</td>
      <td>C:\WINDOWS\Fonts\malgunsl_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>388</td>
      <td>C:\WINDOWS\Fonts\gothicg_.ttf</td>
      <td>GothicG</td>
    </tr>
    <tr>
      <td>389</td>
      <td>C:\WINDOWS\Fonts\swissbi.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>390</td>
      <td>C:\Windows\Fonts\나눔고딕코딩-Bold.ttf</td>
      <td>NanumGothicCoding</td>
    </tr>
    <tr>
      <td>391</td>
      <td>C:\Windows\Fonts\simsun.ttc</td>
      <td>SimSun</td>
    </tr>
    <tr>
      <td>392</td>
      <td>C:\WINDOWS\Fonts\swissl.ttf</td>
      <td>Swis721 Lt BT</td>
    </tr>
    <tr>
      <td>393</td>
      <td>C:\Windows\Fonts\HANDotumB.ttf</td>
      <td>HCR Dotum</td>
    </tr>
    <tr>
      <td>394</td>
      <td>C:\WINDOWS\Fonts\Hancom Gothic Bold.ttf</td>
      <td>Hancom Gothic</td>
    </tr>
    <tr>
      <td>395</td>
      <td>C:\WINDOWS\Fonts\Coure.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>396</td>
      <td>C:\Windows\Fonts\segoeuiz.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>397</td>
      <td>C:\WINDOWS\Fonts\swisse.ttf</td>
      <td>Swis721 Ex BT</td>
    </tr>
    <tr>
      <td>398</td>
      <td>C:\WINDOWS\Fonts\NanumBarunGothicBold.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>399</td>
      <td>C:\WINDOWS\Fonts\ebrimabd.ttf</td>
      <td>Ebrima</td>
    </tr>
    <tr>
      <td>400</td>
      <td>C:\Windows\Fonts\scripts_.ttf</td>
      <td>ScriptS</td>
    </tr>
    <tr>
      <td>401</td>
      <td>C:\WINDOWS\Fonts\HMKMMAG.TTF</td>
      <td>Magic R</td>
    </tr>
    <tr>
      <td>402</td>
      <td>C:\Windows\Fonts\YuGothM.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>403</td>
      <td>C:\WINDOWS\Fonts\DUBAI-LIGHT.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>404</td>
      <td>C:\Windows\Fonts\panroman.ttf</td>
      <td>PanRoman</td>
    </tr>
    <tr>
      <td>405</td>
      <td>C:\WINDOWS\Fonts\umath.ttf</td>
      <td>UniversalMath1 BT</td>
    </tr>
    <tr>
      <td>406</td>
      <td>C:\Windows\Fonts\sylfaen.ttf</td>
      <td>Sylfaen</td>
    </tr>
    <tr>
      <td>407</td>
      <td>C:\WINDOWS\Fonts\H2GPRM.TTF</td>
      <td>HYGraphic-Medium</td>
    </tr>
    <tr>
      <td>408</td>
      <td>C:\Windows\Fonts\dutch.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>409</td>
      <td>C:\Windows\Fonts\swisse.ttf</td>
      <td>Swis721 Ex BT</td>
    </tr>
    <tr>
      <td>410</td>
      <td>C:\Windows\Fonts\sanssb__.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>411</td>
      <td>C:\Windows\Fonts\arialbi.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>412</td>
      <td>C:\WINDOWS\Fonts\lucon.ttf</td>
      <td>Lucida Console</td>
    </tr>
    <tr>
      <td>413</td>
      <td>C:\WINDOWS\Fonts\isoct3__.ttf</td>
      <td>ISOCT3</td>
    </tr>
    <tr>
      <td>414</td>
      <td>C:\Windows\Fonts\HMKMAMI.TTF</td>
      <td>Ami R</td>
    </tr>
    <tr>
      <td>415</td>
      <td>C:\Windows\Fonts\ntailu.ttf</td>
      <td>Microsoft New Tai Lue</td>
    </tr>
    <tr>
      <td>416</td>
      <td>C:\WINDOWS\Fonts\constanz.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>417</td>
      <td>C:\Windows\Fonts\mtproxy5.ttf</td>
      <td>Proxy 5</td>
    </tr>
    <tr>
      <td>418</td>
      <td>C:\WINDOWS\Fonts\symath__.ttf</td>
      <td>Symath</td>
    </tr>
    <tr>
      <td>419</td>
      <td>C:\Windows\Fonts\Hancom Gothic Bold.ttf</td>
      <td>Hancom Gothic</td>
    </tr>
    <tr>
      <td>420</td>
      <td>C:\WINDOWS\Fonts\segoeuil.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>421</td>
      <td>C:\WINDOWS\Fonts\나눔고딕코딩.ttf</td>
      <td>NanumGothicCoding</td>
    </tr>
    <tr>
      <td>422</td>
      <td>C:\Windows\Fonts\ANTQUAB.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>423</td>
      <td>C:\WINDOWS\Fonts\georgiab.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>424</td>
      <td>C:\WINDOWS\Fonts\Candarai.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>425</td>
      <td>C:\WINDOWS\Fonts\H2MJSM.TTF</td>
      <td>HYSinMyeongJo-Medium</td>
    </tr>
    <tr>
      <td>426</td>
      <td>C:\Windows\Fonts\mtproxy8.ttf</td>
      <td>Proxy 8</td>
    </tr>
    <tr>
      <td>427</td>
      <td>C:\WINDOWS\Fonts\marlett.ttf</td>
      <td>Marlett</td>
    </tr>
    <tr>
      <td>428</td>
      <td>C:\WINDOWS\Fonts\sanss___.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>429</td>
      <td>C:\Windows\Fonts\javatext.ttf</td>
      <td>Javanese Text</td>
    </tr>
    <tr>
      <td>430</td>
      <td>C:\Windows\Fonts\Coure.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>431</td>
      <td>C:\Windows\Fonts\bgothl.ttf</td>
      <td>BankGothic Lt BT</td>
    </tr>
    <tr>
      <td>432</td>
      <td>C:\Windows\Fonts\KoPub Batang Bold.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>433</td>
      <td>C:\Windows\Fonts\swisski.ttf</td>
      <td>Swis721 Blk BT</td>
    </tr>
    <tr>
      <td>434</td>
      <td>C:\Windows\Fonts\FiraCode-Regular.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>435</td>
      <td>C:\WINDOWS\Fonts\segoeuiz.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>436</td>
      <td>C:\Windows\Fonts\YuGothL.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>437</td>
      <td>C:\Windows\Fonts\technic_.ttf</td>
      <td>Technic</td>
    </tr>
    <tr>
      <td>438</td>
      <td>C:\WINDOWS\Fonts\taileb.ttf</td>
      <td>Microsoft Tai Le</td>
    </tr>
    <tr>
      <td>439</td>
      <td>C:\Windows\Fonts\corbelb.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>440</td>
      <td>C:\Windows\Fonts\isocpeui.ttf</td>
      <td>ISOCPEUR</td>
    </tr>
    <tr>
      <td>441</td>
      <td>C:\Windows\Fonts\comicbd.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>442</td>
      <td>C:\Windows\Fonts\calibrili.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>443</td>
      <td>C:\WINDOWS\Fonts\swisscki.ttf</td>
      <td>Swis721 BlkCn BT</td>
    </tr>
    <tr>
      <td>444</td>
      <td>C:\WINDOWS\Fonts\cour.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>445</td>
      <td>C:\Windows\Fonts\mmrtext.ttf</td>
      <td>Myanmar Text</td>
    </tr>
    <tr>
      <td>446</td>
      <td>C:\WINDOWS\Fonts\msjhbd.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>447</td>
      <td>C:\Windows\Fonts\swissbo.ttf</td>
      <td>Swis721 BdOul BT</td>
    </tr>
    <tr>
      <td>448</td>
      <td>C:\Windows\Fonts\KoPub Dotum Light.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>449</td>
      <td>C:\Windows\Fonts\HYHWPEQ.TTF</td>
      <td>HyhwpEQ</td>
    </tr>
    <tr>
      <td>450</td>
      <td>C:\Windows\Fonts\comic.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>451</td>
      <td>C:\Windows\Fonts\SitkaI.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>452</td>
      <td>C:\WINDOWS\Fonts\HMKMAMI.TTF</td>
      <td>Ami R</td>
    </tr>
    <tr>
      <td>453</td>
      <td>C:\Windows\Fonts\cambriab.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>454</td>
      <td>C:\WINDOWS\Fonts\ARIALN.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>455</td>
      <td>C:\WINDOWS\Fonts\framdit.ttf</td>
      <td>Franklin Gothic Medium</td>
    </tr>
    <tr>
      <td>456</td>
      <td>C:\WINDOWS\Fonts\H2MKPB.TTF</td>
      <td>HYPMokGak-Bold</td>
    </tr>
    <tr>
      <td>457</td>
      <td>C:\WINDOWS\Fonts\timesbd.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>458</td>
      <td>C:\Windows\Fonts\Candarab.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>459</td>
      <td>C:\Windows\Fonts\impact.ttf</td>
      <td>Impact</td>
    </tr>
    <tr>
      <td>460</td>
      <td>C:\Windows\Fonts\NanumSquareBold.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>461</td>
      <td>C:\WINDOWS\Fonts\HANDotumExt.ttf</td>
      <td>HCR Dotum Ext</td>
    </tr>
    <tr>
      <td>462</td>
      <td>C:\Windows\Fonts\mvboli.ttf</td>
      <td>MV Boli</td>
    </tr>
    <tr>
      <td>463</td>
      <td>C:\Windows\Fonts\constani.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>464</td>
      <td>C:\WINDOWS\Fonts\courbi.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>465</td>
      <td>C:\WINDOWS\Fonts\NanumSquareRoundB.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>466</td>
      <td>C:\WINDOWS\Fonts\HANBatang.ttf</td>
      <td>HCR Batang</td>
    </tr>
    <tr>
      <td>467</td>
      <td>C:\Windows\Fonts\msjhl.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>468</td>
      <td>C:\Windows\Fonts\txt_____.ttf</td>
      <td>Txt</td>
    </tr>
    <tr>
      <td>469</td>
      <td>C:\Windows\Fonts\symbol.ttf</td>
      <td>Symbol</td>
    </tr>
    <tr>
      <td>470</td>
      <td>C:\WINDOWS\Fonts\arialbd.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>471</td>
      <td>C:\Windows\Fonts\dutchb.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>472</td>
      <td>C:\Windows\Fonts\swissel.ttf</td>
      <td>Swis721 LtEx BT</td>
    </tr>
    <tr>
      <td>473</td>
      <td>C:\WINDOWS\Fonts\malgunbd_0.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>474</td>
      <td>C:\Windows\Fonts\HANDotumExt.ttf</td>
      <td>HCR Dotum Ext</td>
    </tr>
    <tr>
      <td>475</td>
      <td>C:\Windows\Fonts\corbelz.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>476</td>
      <td>C:\Windows\Fonts\H2PORM.TTF</td>
      <td>HYPost-Medium</td>
    </tr>
    <tr>
      <td>477</td>
      <td>C:\Windows\Fonts\seguisb.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>478</td>
      <td>C:\Windows\Fonts\gothice_.ttf</td>
      <td>GothicE</td>
    </tr>
    <tr>
      <td>479</td>
      <td>C:\WINDOWS\Fonts\txt_____.ttf</td>
      <td>Txt</td>
    </tr>
    <tr>
      <td>480</td>
      <td>C:\Windows\Fonts\ebrimabd.ttf</td>
      <td>Ebrima</td>
    </tr>
    <tr>
      <td>481</td>
      <td>C:\Windows\Fonts\HMFMPYUN.TTF</td>
      <td>Pyunji R</td>
    </tr>
    <tr>
      <td>482</td>
      <td>C:\WINDOWS\Fonts\FiraCode-Bold.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>483</td>
      <td>C:\Windows\Fonts\msjh.ttc</td>
      <td>Microsoft JhengHei</td>
    </tr>
    <tr>
      <td>484</td>
      <td>C:\WINDOWS\Fonts\GENISO.ttf</td>
      <td>GENISO</td>
    </tr>
    <tr>
      <td>485</td>
      <td>C:\WINDOWS\Fonts\consola.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>486</td>
      <td>C:\WINDOWS\Fonts\tahoma.ttf</td>
      <td>Tahoma</td>
    </tr>
    <tr>
      <td>487</td>
      <td>C:\WINDOWS\Fonts\techb___.ttf</td>
      <td>TechnicBold</td>
    </tr>
    <tr>
      <td>488</td>
      <td>C:\WINDOWS\Fonts\symap___.ttf</td>
      <td>Symap</td>
    </tr>
    <tr>
      <td>489</td>
      <td>C:\WINDOWS\Fonts\segoeuii.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>490</td>
      <td>C:\WINDOWS\Fonts\msyi.ttf</td>
      <td>Microsoft Yi Baiti</td>
    </tr>
    <tr>
      <td>491</td>
      <td>C:\Windows\Fonts\lucon.ttf</td>
      <td>Lucida Console</td>
    </tr>
    <tr>
      <td>492</td>
      <td>C:\WINDOWS\Fonts\ANTQUABI.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>493</td>
      <td>C:\Windows\Fonts\SitkaB.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>494</td>
      <td>C:\Windows\Fonts\compi.ttf</td>
      <td>CommercialPi BT</td>
    </tr>
    <tr>
      <td>495</td>
      <td>C:\WINDOWS\Fonts\segoepr.ttf</td>
      <td>Segoe Print</td>
    </tr>
    <tr>
      <td>496</td>
      <td>C:\WINDOWS\Fonts\GOTHIC.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>497</td>
      <td>C:\Windows\Fonts\framd.ttf</td>
      <td>Franklin Gothic Medium</td>
    </tr>
    <tr>
      <td>498</td>
      <td>C:\WINDOWS\Fonts\mtproxy3.ttf</td>
      <td>Proxy 3</td>
    </tr>
    <tr>
      <td>499</td>
      <td>C:\Windows\Fonts\segoeprb.ttf</td>
      <td>Segoe Print</td>
    </tr>
    <tr>
      <td>500</td>
      <td>C:\Windows\Fonts\timesi.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>501</td>
      <td>C:\WINDOWS\Fonts\swissi.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>502</td>
      <td>C:\WINDOWS\Fonts\corbeli.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>503</td>
      <td>C:\WINDOWS\Fonts\mtproxy4.ttf</td>
      <td>Proxy 4</td>
    </tr>
    <tr>
      <td>504</td>
      <td>C:\WINDOWS\Fonts\ARIALNB.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>505</td>
      <td>C:\Windows\Fonts\sansso__.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>506</td>
      <td>C:\WINDOWS\Fonts\Gabriola.ttf</td>
      <td>Gabriola</td>
    </tr>
    <tr>
      <td>507</td>
      <td>C:\Windows\Fonts\NanumBarunpenRegular.ttf</td>
      <td>NanumBarunpen</td>
    </tr>
    <tr>
      <td>508</td>
      <td>C:\WINDOWS\Fonts\romant__.ttf</td>
      <td>RomanT</td>
    </tr>
    <tr>
      <td>509</td>
      <td>C:\WINDOWS\Fonts\trebucbd.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>510</td>
      <td>C:\WINDOWS\Fonts\DUBAI-MEDIUM.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>511</td>
      <td>C:\Windows\Fonts\symeteo_.ttf</td>
      <td>Symeteo</td>
    </tr>
    <tr>
      <td>512</td>
      <td>C:\WINDOWS\Fonts\symbol.ttf</td>
      <td>Symbol</td>
    </tr>
    <tr>
      <td>513</td>
      <td>C:\Windows\Fonts\gdt_____.ttf</td>
      <td>GDT</td>
    </tr>
    <tr>
      <td>514</td>
      <td>C:\Windows\Fonts\GOTHICB.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>515</td>
      <td>C:\WINDOWS\Fonts\SitkaB.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>516</td>
      <td>C:\Windows\Fonts\mtproxy7.ttf</td>
      <td>Proxy 7</td>
    </tr>
    <tr>
      <td>517</td>
      <td>C:\Windows\Fonts\SymbM.ttf</td>
      <td>SymbolMono BT</td>
    </tr>
    <tr>
      <td>518</td>
      <td>C:\Windows\Fonts\romantic.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>519</td>
      <td>C:\Windows\Fonts\seguibli.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>520</td>
      <td>C:\Windows\Fonts\symusic_.ttf</td>
      <td>Symusic</td>
    </tr>
    <tr>
      <td>521</td>
      <td>C:\WINDOWS\Fonts\gothice_.ttf</td>
      <td>GothicE</td>
    </tr>
    <tr>
      <td>522</td>
      <td>C:\Windows\Fonts\malgun.ttf</td>
      <td>Malgun Gothic</td>
    </tr>
    <tr>
      <td>523</td>
      <td>C:\WINDOWS\Fonts\trebuc.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>524</td>
      <td>C:\WINDOWS\Fonts\complex_.ttf</td>
      <td>Complex</td>
    </tr>
    <tr>
      <td>525</td>
      <td>C:\Windows\Fonts\AcadEref.ttf</td>
      <td>AcadEref</td>
    </tr>
    <tr>
      <td>526</td>
      <td>C:\WINDOWS\Fonts\FiraCode-Light.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>527</td>
      <td>C:\Windows\Fonts\swissbi.ttf</td>
      <td>Swis721 BT</td>
    </tr>
    <tr>
      <td>528</td>
      <td>C:\Windows\Fonts\KoPub Dotum Bold.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>529</td>
      <td>C:\WINDOWS\Fonts\isocteui.ttf</td>
      <td>ISOCTEUR</td>
    </tr>
    <tr>
      <td>530</td>
      <td>C:\WINDOWS\Fonts\monosbi.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>531</td>
      <td>C:\WINDOWS\Fonts\mtproxy1.ttf</td>
      <td>Proxy 1</td>
    </tr>
    <tr>
      <td>532</td>
      <td>C:\Windows\Fonts\calibrib.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>533</td>
      <td>C:\Windows\Fonts\D2Coding-Ver1.3-20171129.ttf</td>
      <td>D2Coding</td>
    </tr>
    <tr>
      <td>534</td>
      <td>C:\WINDOWS\Fonts\KoPub Batang Bold.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>535</td>
      <td>C:\Windows\Fonts\ARIALN.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>536</td>
      <td>C:\Windows\Fonts\phagspab.ttf</td>
      <td>Microsoft PhagsPa</td>
    </tr>
    <tr>
      <td>537</td>
      <td>C:\Windows\Fonts\msyhbd.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>538</td>
      <td>C:\Windows\Fonts\timesbi.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>539</td>
      <td>C:\WINDOWS\Fonts\HanSantteutDotumBold.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>540</td>
      <td>C:\WINDOWS\Fonts\compi.ttf</td>
      <td>CommercialPi BT</td>
    </tr>
    <tr>
      <td>541</td>
      <td>C:\WINDOWS\Fonts\mtproxy5.ttf</td>
      <td>Proxy 5</td>
    </tr>
    <tr>
      <td>542</td>
      <td>C:\WINDOWS\Fonts\NanumBarunGothic.ttf</td>
      <td>NanumBarunGothic</td>
    </tr>
    <tr>
      <td>543</td>
      <td>C:\WINDOWS\Fonts\swisski.ttf</td>
      <td>Swis721 Blk BT</td>
    </tr>
    <tr>
      <td>544</td>
      <td>C:\Windows\Fonts\CENTURY.TTF</td>
      <td>Century</td>
    </tr>
    <tr>
      <td>545</td>
      <td>C:\Windows\Fonts\Candaral.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>546</td>
      <td>C:\WINDOWS\Fonts\sylfaen.ttf</td>
      <td>Sylfaen</td>
    </tr>
    <tr>
      <td>547</td>
      <td>C:\Windows\Fonts\swissl.ttf</td>
      <td>Swis721 Lt BT</td>
    </tr>
    <tr>
      <td>548</td>
      <td>C:\WINDOWS\Fonts\H2GTRM.TTF</td>
      <td>HYGothic-Medium</td>
    </tr>
    <tr>
      <td>549</td>
      <td>C:\Windows\Fonts\LeelaUIb.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>550</td>
      <td>C:\Windows\Fonts\H2SA1M.TTF</td>
      <td>HYShortSamul-Medium</td>
    </tr>
    <tr>
      <td>551</td>
      <td>C:\Windows\Fonts\constanb.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>552</td>
      <td>C:\Windows\Fonts\phagspa.ttf</td>
      <td>Microsoft PhagsPa</td>
    </tr>
    <tr>
      <td>553</td>
      <td>C:\WINDOWS\Fonts\technic_.ttf</td>
      <td>Technic</td>
    </tr>
    <tr>
      <td>554</td>
      <td>C:\Windows\Fonts\swissck.ttf</td>
      <td>Swis721 BlkCn BT</td>
    </tr>
    <tr>
      <td>555</td>
      <td>C:\WINDOWS\Fonts\KoPub Batang Medium.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>556</td>
      <td>C:\WINDOWS\Fonts\NanumMyeongjoBold.ttf</td>
      <td>NanumMyeongjo</td>
    </tr>
    <tr>
      <td>557</td>
      <td>C:\WINDOWS\Fonts\scriptc_.ttf</td>
      <td>ScriptC</td>
    </tr>
    <tr>
      <td>558</td>
      <td>C:\WINDOWS\Fonts\tahomabd.ttf</td>
      <td>Tahoma</td>
    </tr>
    <tr>
      <td>559</td>
      <td>C:\WINDOWS\Fonts\KoPub Batang Light.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>560</td>
      <td>C:\Windows\Fonts\NanumSquareRoundB.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>561</td>
      <td>C:\WINDOWS\Fonts\simsunb.ttf</td>
      <td>SimSun-ExtB</td>
    </tr>
    <tr>
      <td>562</td>
      <td>C:\WINDOWS\Fonts\GARABD.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>563</td>
      <td>C:\Windows\Fonts\cour.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>564</td>
      <td>C:\WINDOWS\Fonts\CENTURY.TTF</td>
      <td>Century</td>
    </tr>
    <tr>
      <td>565</td>
      <td>C:\WINDOWS\Fonts\나눔고딕코딩-Bold.ttf</td>
      <td>NanumGothicCoding</td>
    </tr>
    <tr>
      <td>566</td>
      <td>C:\WINDOWS\Fonts\corbelb.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>567</td>
      <td>C:\Windows\Fonts\corbeli.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>568</td>
      <td>C:\WINDOWS\Fonts\sanssb__.ttf</td>
      <td>SansSerif</td>
    </tr>
    <tr>
      <td>569</td>
      <td>C:\Windows\Fonts\CoureB.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>570</td>
      <td>C:\WINDOWS\Fonts\H2GTRE.TTF</td>
      <td>HYGothic-Extra</td>
    </tr>
    <tr>
      <td>571</td>
      <td>C:\WINDOWS\Fonts\SitkaI.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>572</td>
      <td>C:\WINDOWS\Fonts\constan.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>573</td>
      <td>C:\Windows\Fonts\monos.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>574</td>
      <td>C:\WINDOWS\Fonts\seguisym.ttf</td>
      <td>Segoe UI Symbol</td>
    </tr>
    <tr>
      <td>575</td>
      <td>C:\WINDOWS\Fonts\swisscli.ttf</td>
      <td>Swis721 LtCn BT</td>
    </tr>
    <tr>
      <td>576</td>
      <td>C:\Windows\Fonts\segoeuil.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>577</td>
      <td>C:\Windows\Fonts\GOTHICI.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>578</td>
      <td>C:\WINDOWS\Fonts\Inkfree.ttf</td>
      <td>Ink Free</td>
    </tr>
    <tr>
      <td>579</td>
      <td>C:\WINDOWS\Fonts\AMDT_Symbols.ttf</td>
      <td>AmdtSymbols</td>
    </tr>
    <tr>
      <td>580</td>
      <td>C:\WINDOWS\Fonts\gadugib.ttf</td>
      <td>Gadugi</td>
    </tr>
    <tr>
      <td>581</td>
      <td>C:\Windows\Fonts\BOOKOSBI.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>582</td>
      <td>C:\WINDOWS\Fonts\palabi.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>583</td>
      <td>C:\Windows\Fonts\swisscli.ttf</td>
      <td>Swis721 LtCn BT</td>
    </tr>
    <tr>
      <td>584</td>
      <td>C:\WINDOWS\Fonts\H2SA1M.TTF</td>
      <td>HYShortSamul-Medium</td>
    </tr>
    <tr>
      <td>585</td>
      <td>C:\WINDOWS\Fonts\WINGDNG2.TTF</td>
      <td>Wingdings 2</td>
    </tr>
    <tr>
      <td>586</td>
      <td>C:\Windows\Fonts\H2GSRB.TTF</td>
      <td>HYGungSo-Bold</td>
    </tr>
    <tr>
      <td>587</td>
      <td>C:\WINDOWS\Fonts\BSSYM7.TTF</td>
      <td>Bookshelf Symbol 7</td>
    </tr>
    <tr>
      <td>588</td>
      <td>C:\Windows\Fonts\gadugi.ttf</td>
      <td>Gadugi</td>
    </tr>
    <tr>
      <td>589</td>
      <td>C:\Windows\Fonts\counb___.ttf</td>
      <td>CountryBlueprint</td>
    </tr>
    <tr>
      <td>590</td>
      <td>C:\WINDOWS\Fonts\segoescb.ttf</td>
      <td>Segoe Script</td>
    </tr>
    <tr>
      <td>591</td>
      <td>C:\WINDOWS\Fonts\NirmalaS.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>592</td>
      <td>C:\WINDOWS\Fonts\HanSantteutDotum-Regular.ttf</td>
      <td>Han Santteut Dotum</td>
    </tr>
    <tr>
      <td>593</td>
      <td>C:\Windows\Fonts\HANBatangB.ttf</td>
      <td>HCR Batang</td>
    </tr>
    <tr>
      <td>594</td>
      <td>C:\Windows\Fonts\YuGothB.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>595</td>
      <td>C:\Windows\Fonts\cityb___.ttf</td>
      <td>CityBlueprint</td>
    </tr>
    <tr>
      <td>596</td>
      <td>C:\WINDOWS\Fonts\italicc_.ttf</td>
      <td>ItalicC</td>
    </tr>
    <tr>
      <td>597</td>
      <td>C:\WINDOWS\Fonts\OUTLOOK.TTF</td>
      <td>MS Outlook</td>
    </tr>
    <tr>
      <td>598</td>
      <td>C:\WINDOWS\Fonts\swissel.ttf</td>
      <td>Swis721 LtEx BT</td>
    </tr>
    <tr>
      <td>599</td>
      <td>C:\WINDOWS\Fonts\symusic_.ttf</td>
      <td>Symusic</td>
    </tr>
    <tr>
      <td>600</td>
      <td>C:\Windows\Fonts\webdings.ttf</td>
      <td>Webdings</td>
    </tr>
    <tr>
      <td>601</td>
      <td>C:\Windows\Fonts\HANBatangExtB.ttf</td>
      <td>HCR Batang ExtB</td>
    </tr>
    <tr>
      <td>602</td>
      <td>C:\WINDOWS\Fonts\Sitka.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>603</td>
      <td>C:\Windows\Fonts\DUBAI-BOLD.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>604</td>
      <td>C:\Windows\Fonts\ariblk.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>605</td>
      <td>C:\WINDOWS\Fonts\italict_.ttf</td>
      <td>ItalicT</td>
    </tr>
    <tr>
      <td>606</td>
      <td>C:\Windows\Fonts\romai___.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>607</td>
      <td>C:\WINDOWS\Fonts\LeelaUIb.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>608</td>
      <td>C:\WINDOWS\Fonts\georgia.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>609</td>
      <td>C:\WINDOWS\Fonts\GOTHICBI.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>610</td>
      <td>C:\Windows\Fonts\monosb.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>611</td>
      <td>C:\Windows\Fonts\corbell.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>612</td>
      <td>C:\WINDOWS\Fonts\NanumSquareRoundL.ttf</td>
      <td>NanumSquareRound</td>
    </tr>
    <tr>
      <td>613</td>
      <td>C:\WINDOWS\Fonts\GOTHICI.TTF</td>
      <td>Century Gothic</td>
    </tr>
    <tr>
      <td>614</td>
      <td>C:\Windows\Fonts\seguili.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>615</td>
      <td>C:\WINDOWS\Fonts\msyhbd.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>616</td>
      <td>C:\Windows\Fonts\mtproxy4.ttf</td>
      <td>Proxy 4</td>
    </tr>
    <tr>
      <td>617</td>
      <td>C:\WINDOWS\Fonts\segoesc.ttf</td>
      <td>Segoe Script</td>
    </tr>
    <tr>
      <td>618</td>
      <td>C:\Windows\Fonts\Candaraz.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>619</td>
      <td>C:\Windows\Fonts\comicz.ttf</td>
      <td>Comic Sans MS</td>
    </tr>
    <tr>
      <td>620</td>
      <td>C:\Windows\Fonts\l_10646.ttf</td>
      <td>Lucida Sans Unicode</td>
    </tr>
    <tr>
      <td>621</td>
      <td>C:\Windows\Fonts\GARAIT.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>622</td>
      <td>C:\Windows\Fonts\OUTLOOK.TTF</td>
      <td>MS Outlook</td>
    </tr>
    <tr>
      <td>623</td>
      <td>C:\WINDOWS\Fonts\cambriaz.ttf</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>624</td>
      <td>C:\WINDOWS\Fonts\segoeui.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>625</td>
      <td>C:\WINDOWS\Fonts\verdanaz.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>626</td>
      <td>C:\WINDOWS\Fonts\gulim.ttc</td>
      <td>Gulim</td>
    </tr>
    <tr>
      <td>627</td>
      <td>C:\WINDOWS\Fonts\Nirmala.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>628</td>
      <td>C:\Windows\Fonts\consolab.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>629</td>
      <td>C:\Windows\Fonts\corbelli.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>630</td>
      <td>C:\WINDOWS\Fonts\mtproxy2.ttf</td>
      <td>Proxy 2</td>
    </tr>
    <tr>
      <td>631</td>
      <td>C:\Windows\Fonts\trebucbi.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>632</td>
      <td>C:\WINDOWS\Fonts\constanb.ttf</td>
      <td>Constantia</td>
    </tr>
    <tr>
      <td>633</td>
      <td>C:\Windows\Fonts\LeelawUI.ttf</td>
      <td>Leelawadee UI</td>
    </tr>
    <tr>
      <td>634</td>
      <td>C:\Windows\Fonts\supef___.ttf</td>
      <td>SuperFrench</td>
    </tr>
    <tr>
      <td>635</td>
      <td>C:\WINDOWS\Fonts\isocp___.ttf</td>
      <td>ISOCP</td>
    </tr>
    <tr>
      <td>636</td>
      <td>C:\WINDOWS\Fonts\romai___.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>637</td>
      <td>C:\Windows\Fonts\tahomabd.ttf</td>
      <td>Tahoma</td>
    </tr>
    <tr>
      <td>638</td>
      <td>C:\Windows\Fonts\KoPub Batang Light.ttf</td>
      <td>KoPubBatang</td>
    </tr>
    <tr>
      <td>639</td>
      <td>C:\Windows\Fonts\bahnschrift.ttf</td>
      <td>Bahnschrift</td>
    </tr>
    <tr>
      <td>640</td>
      <td>C:\Windows\Fonts\swisscl.ttf</td>
      <td>Swis721 LtCn BT</td>
    </tr>
    <tr>
      <td>641</td>
      <td>C:\WINDOWS\Fonts\calibrib.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>642</td>
      <td>C:\WINDOWS\Fonts\H2GSRB.TTF</td>
      <td>HYGungSo-Bold</td>
    </tr>
    <tr>
      <td>643</td>
      <td>C:\Windows\Fonts\verdanab.ttf</td>
      <td>Verdana</td>
    </tr>
    <tr>
      <td>644</td>
      <td>C:\WINDOWS\Fonts\corbelli.ttf</td>
      <td>Corbel</td>
    </tr>
    <tr>
      <td>645</td>
      <td>C:\WINDOWS\Fonts\REFSAN.TTF</td>
      <td>MS Reference Sans Serif</td>
    </tr>
    <tr>
      <td>646</td>
      <td>C:\WINDOWS\Fonts\mmrtextb.ttf</td>
      <td>Myanmar Text</td>
    </tr>
    <tr>
      <td>647</td>
      <td>C:\Windows\Fonts\msyi.ttf</td>
      <td>Microsoft Yi Baiti</td>
    </tr>
    <tr>
      <td>648</td>
      <td>C:\WINDOWS\Fonts\HMFMPYUN.TTF</td>
      <td>Pyunji R</td>
    </tr>
    <tr>
      <td>649</td>
      <td>C:\WINDOWS\Fonts\segoeuisl.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>650</td>
      <td>C:\WINDOWS\Fonts\seguibl.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>651</td>
      <td>C:\Windows\Fonts\FiraCode-Retina.ttf</td>
      <td>Fira Code</td>
    </tr>
    <tr>
      <td>652</td>
      <td>C:\Windows\Fonts\segoescb.ttf</td>
      <td>Segoe Script</td>
    </tr>
    <tr>
      <td>653</td>
      <td>C:\Windows\Fonts\AMDT_Symbols.ttf</td>
      <td>AmdtSymbols</td>
    </tr>
    <tr>
      <td>654</td>
      <td>C:\Windows\Fonts\consola.ttf</td>
      <td>Consolas</td>
    </tr>
    <tr>
      <td>655</td>
      <td>C:\Windows\Fonts\CoureBI.ttf</td>
      <td>Courier10 BT</td>
    </tr>
    <tr>
      <td>656</td>
      <td>C:\WINDOWS\Fonts\swissko.ttf</td>
      <td>Swis721 BlkOul BT</td>
    </tr>
    <tr>
      <td>657</td>
      <td>C:\WINDOWS\Fonts\swissek.ttf</td>
      <td>Swis721 BlkEx BT</td>
    </tr>
    <tr>
      <td>658</td>
      <td>C:\WINDOWS\Fonts\calibrii.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>659</td>
      <td>C:\Windows\Fonts\NanumSquareLight.ttf</td>
      <td>NanumSquare</td>
    </tr>
    <tr>
      <td>660</td>
      <td>C:\WINDOWS\Fonts\romab___.ttf</td>
      <td>Romantic</td>
    </tr>
    <tr>
      <td>661</td>
      <td>C:\WINDOWS\Fonts\arial.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>662</td>
      <td>C:\Windows\Fonts\timesbd.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>663</td>
      <td>C:\Windows\Fonts\seguisbi.ttf</td>
      <td>Segoe UI</td>
    </tr>
    <tr>
      <td>664</td>
      <td>C:\Windows\Fonts\mmrtextb.ttf</td>
      <td>Myanmar Text</td>
    </tr>
    <tr>
      <td>665</td>
      <td>C:\WINDOWS\Fonts\cambria.ttc</td>
      <td>Cambria</td>
    </tr>
    <tr>
      <td>666</td>
      <td>C:\WINDOWS\Fonts\GARAIT.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>667</td>
      <td>C:\WINDOWS\Fonts\isocpeur.ttf</td>
      <td>ISOCPEUR</td>
    </tr>
    <tr>
      <td>668</td>
      <td>C:\WINDOWS\Fonts\palai.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>669</td>
      <td>C:\Windows\Fonts\swissk.ttf</td>
      <td>Swis721 Blk BT</td>
    </tr>
    <tr>
      <td>670</td>
      <td>C:\Windows\Fonts\Sitka.ttc</td>
      <td>Sitka Small</td>
    </tr>
    <tr>
      <td>671</td>
      <td>C:\WINDOWS\Fonts\H2PORM.TTF</td>
      <td>HYPost-Medium</td>
    </tr>
    <tr>
      <td>672</td>
      <td>C:\Windows\Fonts\trebuc.ttf</td>
      <td>Trebuchet MS</td>
    </tr>
    <tr>
      <td>673</td>
      <td>C:\Windows\Fonts\MTCORSVA.TTF</td>
      <td>Monotype Corsiva</td>
    </tr>
    <tr>
      <td>674</td>
      <td>C:\Windows\Fonts\palabi.ttf</td>
      <td>Palatino Linotype</td>
    </tr>
    <tr>
      <td>675</td>
      <td>C:\Windows\Fonts\H2GPRM.TTF</td>
      <td>HYGraphic-Medium</td>
    </tr>
    <tr>
      <td>676</td>
      <td>C:\Windows\Fonts\complex_.ttf</td>
      <td>Complex</td>
    </tr>
    <tr>
      <td>677</td>
      <td>C:\Windows\Fonts\georgiaz.ttf</td>
      <td>Georgia</td>
    </tr>
    <tr>
      <td>678</td>
      <td>C:\WINDOWS\Fonts\Candarab.ttf</td>
      <td>Candara</td>
    </tr>
    <tr>
      <td>679</td>
      <td>C:\Windows\Fonts\ANTQUABI.TTF</td>
      <td>Book Antiqua</td>
    </tr>
    <tr>
      <td>680</td>
      <td>C:\WINDOWS\Fonts\monos.ttf</td>
      <td>Monospac821 BT</td>
    </tr>
    <tr>
      <td>681</td>
      <td>C:\WINDOWS\Fonts\NanumGothicBold.ttf</td>
      <td>NanumGothic</td>
    </tr>
    <tr>
      <td>682</td>
      <td>C:\WINDOWS\Fonts\panroman.ttf</td>
      <td>PanRoman</td>
    </tr>
    <tr>
      <td>683</td>
      <td>C:\Windows\Fonts\msyh.ttc</td>
      <td>Microsoft YaHei</td>
    </tr>
    <tr>
      <td>684</td>
      <td>C:\Windows\Fonts\isocp2__.ttf</td>
      <td>ISOCP2</td>
    </tr>
    <tr>
      <td>685</td>
      <td>C:\WINDOWS\Fonts\monbaiti.ttf</td>
      <td>Mongolian Baiti</td>
    </tr>
    <tr>
      <td>686</td>
      <td>C:\WINDOWS\Fonts\swisseb.ttf</td>
      <td>Swis721 Ex BT</td>
    </tr>
    <tr>
      <td>687</td>
      <td>C:\Windows\Fonts\ARIALNB.TTF</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>688</td>
      <td>C:\Windows\Fonts\mtproxy2.ttf</td>
      <td>Proxy 2</td>
    </tr>
    <tr>
      <td>689</td>
      <td>C:\Windows\Fonts\GARA.TTF</td>
      <td>Garamond</td>
    </tr>
    <tr>
      <td>690</td>
      <td>C:\Windows\Fonts\taile.ttf</td>
      <td>Microsoft Tai Le</td>
    </tr>
    <tr>
      <td>691</td>
      <td>C:\Windows\Fonts\Nirmala.ttf</td>
      <td>Nirmala UI</td>
    </tr>
    <tr>
      <td>692</td>
      <td>C:\WINDOWS\Fonts\greekc__.ttf</td>
      <td>GreekC</td>
    </tr>
    <tr>
      <td>693</td>
      <td>C:\Windows\Fonts\HMFMOLD.TTF</td>
      <td>Yet R</td>
    </tr>
    <tr>
      <td>694</td>
      <td>C:\WINDOWS\Fonts\timesi.ttf</td>
      <td>Times New Roman</td>
    </tr>
    <tr>
      <td>695</td>
      <td>C:\WINDOWS\Fonts\ariblk.ttf</td>
      <td>Arial</td>
    </tr>
    <tr>
      <td>696</td>
      <td>C:\WINDOWS\Fonts\H2HDRM.TTF</td>
      <td>HYHeadLine-Medium</td>
    </tr>
    <tr>
      <td>697</td>
      <td>C:\WINDOWS\Fonts\l_10646.ttf</td>
      <td>Lucida Sans Unicode</td>
    </tr>
    <tr>
      <td>698</td>
      <td>C:\WINDOWS\Fonts\HANDotumB.ttf</td>
      <td>HCR Dotum</td>
    </tr>
    <tr>
      <td>699</td>
      <td>C:\Windows\Fonts\DUBAI-LIGHT.TTF</td>
      <td>Dubai</td>
    </tr>
    <tr>
      <td>700</td>
      <td>C:\Windows\Fonts\calibril.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>701</td>
      <td>C:\Windows\Fonts\swissko.ttf</td>
      <td>Swis721 BlkOul BT</td>
    </tr>
    <tr>
      <td>702</td>
      <td>C:\Windows\Fonts\romant__.ttf</td>
      <td>RomanT</td>
    </tr>
    <tr>
      <td>703</td>
      <td>C:\Windows\Fonts\courbd.ttf</td>
      <td>Courier New</td>
    </tr>
    <tr>
      <td>704</td>
      <td>C:\WINDOWS\Fonts\SymbP.ttf</td>
      <td>SymbolProp BT</td>
    </tr>
    <tr>
      <td>705</td>
      <td>C:\WINDOWS\Fonts\BOOKOS.TTF</td>
      <td>Bookman Old Style</td>
    </tr>
    <tr>
      <td>706</td>
      <td>C:\WINDOWS\Fonts\HMFMMUEX.TTC</td>
      <td>MoeumT R</td>
    </tr>
    <tr>
      <td>707</td>
      <td>C:\Windows\Fonts\calibriz.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>708</td>
      <td>C:\Windows\Fonts\YuGothR.ttc</td>
      <td>Yu Gothic</td>
    </tr>
    <tr>
      <td>709</td>
      <td>C:\WINDOWS\Fonts\HATTEN.TTF</td>
      <td>Haettenschweiler</td>
    </tr>
    <tr>
      <td>710</td>
      <td>C:\WINDOWS\Fonts\dutchb.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>711</td>
      <td>C:\Windows\Fonts\swisseb.ttf</td>
      <td>Swis721 Ex BT</td>
    </tr>
    <tr>
      <td>712</td>
      <td>C:\Windows\Fonts\isocp___.ttf</td>
      <td>ISOCP</td>
    </tr>
    <tr>
      <td>713</td>
      <td>C:\WINDOWS\Fonts\REFSPCL.TTF</td>
      <td>MS Reference Specialty</td>
    </tr>
    <tr>
      <td>714</td>
      <td>C:\Windows\Fonts\HANBatangExtBB.ttf</td>
      <td>HCR Batang ExtB</td>
    </tr>
    <tr>
      <td>715</td>
      <td>C:\Windows\Fonts\BSSYM7.TTF</td>
      <td>Bookshelf Symbol 7</td>
    </tr>
    <tr>
      <td>716</td>
      <td>C:\WINDOWS\Fonts\NanumBarunpenBold.ttf</td>
      <td>NanumBarunpen</td>
    </tr>
    <tr>
      <td>717</td>
      <td>C:\WINDOWS\Fonts\monotxt_.ttf</td>
      <td>Monotxt</td>
    </tr>
    <tr>
      <td>718</td>
      <td>C:\Windows\Fonts\NanumBrush.ttf</td>
      <td>Nanum Brush Script</td>
    </tr>
    <tr>
      <td>719</td>
      <td>C:\WINDOWS\Fonts\gadugi.ttf</td>
      <td>Gadugi</td>
    </tr>
    <tr>
      <td>720</td>
      <td>C:\Windows\Fonts\KoPub Dotum Medium.ttf</td>
      <td>KoPubDotum</td>
    </tr>
    <tr>
      <td>721</td>
      <td>C:\WINDOWS\Fonts\dutch.ttf</td>
      <td>Dutch801 Rm BT</td>
    </tr>
    <tr>
      <td>722</td>
      <td>C:\Windows\Fonts\vinet.ttf</td>
      <td>Vineta BT</td>
    </tr>
    <tr>
      <td>723</td>
      <td>C:\WINDOWS\Fonts\MTCORSVA.TTF</td>
      <td>Monotype Corsiva</td>
    </tr>
    <tr>
      <td>724</td>
      <td>C:\WINDOWS\Fonts\NanumPen.ttf</td>
      <td>Nanum Pen Script</td>
    </tr>
    <tr>
      <td>725</td>
      <td>C:\WINDOWS\Fonts\mmrtext.ttf</td>
      <td>Myanmar Text</td>
    </tr>
    <tr>
      <td>726</td>
      <td>C:\WINDOWS\Fonts\mtproxy7.ttf</td>
      <td>Proxy 7</td>
    </tr>
    <tr>
      <td>727</td>
      <td>C:\Windows\Fonts\calibri.ttf</td>
      <td>Calibri</td>
    </tr>
    <tr>
      <td>728</td>
      <td>C:\Windows\Fonts\SymbC.ttf</td>
      <td>CATIA Symbols</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
