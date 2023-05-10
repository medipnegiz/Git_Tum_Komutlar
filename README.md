# Git and Git Flow Cheat Sheet 
________________________________________
 
## Index

*	[Kurulum](#kurulum)
*	[Yapılandırma](#yapilandirma)
*	Oluşturma
*	Yerel Değişiklikler
*	Arama
*	Commit Geçmişi
*	Branches & Tags(Etiketler)
*	Güncelleştirme & Yayınlama
*	Merge(Birleştirme) & Rebase
*	Geri Alma
*	Git Flow
________________________________________

## Kurulum

Mevcut ayarları göstermek:
```bash
git config --list
```

Repository(depo) ayarlarını göstermek:
```bash
git config --local --list
```

Global ayarları göstermek:
```bash
git config --global --list
```

Sistem ayarlarını göstermek:
```bash
git config --system --list
```

Sürüm geçmişinde gözükecek adı belirlemek:
```bash
git config --global user.name “[firstname lastname]”
```

Sürüm geçmişinde ilişkilendirilecek e-postayı belirlemek:
```bash
git config --global user.email “[valid-email]”
```

Otomatik komut satırı renklendirmesini ayarlamak:
```bash
git config --global color.ui auto
```

Commitler için global yazı editörünü ayarlamak:
```bash
git config --global core.editor vi
```

________________________________________

## Yapılandırma

Repositorye(depoya) özgü yapılandırma dosyası [--local]:
```bash
<repo>/.git/config
```

Kullanıcıya özel yapılandırma dosyası [--global]:
```bash
~/.gitconfig
```

Sistem genelinde yapılandırma dosyası [--system]:
```bash
/etc/gitconfig
```

________________________________________

## Oluşturma

Var olan bir repositoryi(depoyu) klonlama:
```bash
git clone ssh://user@domain.com/repo.git
```

Yeni bir yerel repository(depo) oluşturma:
```bash
git init
```

Belirli dizinde yerel repository(depo) oluşturma:
```bash
git init <directory>
```

<hr>

## Yerel Değişiklikler

##### Çalışılan dizindeki dosyaların değişimi:
```bash
git status
```

##### İzlenen dosyalardaki değişiklikler:
```bash
git diff
```

##### Tüm güncel değişiklikleri sonraki commite ekleme:
```bash
git add .
```

##### Sonraki commite &lt;dosyasındaki&gt; bazı değişikleri ekleme:
```bash
git add -p
```

##### Tüm izlenen dosyalardaki yerel değişiklikleri Commitleme:
```bash
git commit -a
```

##### Önceden hazırlanan değişiklikleri commitleme:
```bash
git commit
```

##### Mesaj ile commitleme:
```bash
git commit -m 'message here'
```

##### Önceki belli bir tarihe commitleme:
```bash
git commit --date="date --date='n day ago'" -am "Commit Message"
```

##### Son commiti değiştirme:<br>
###### Yayınlanan commite değişiklik yapmayın!
```bash
git commit --amend
```

##### Mevcut branchteki kaydedilmemiş commitleri diğer bazı branchlere taşıma:
```bash
git stash git checkout branch2 git stash pop
```

##### Saklanan değişiklikleri mevcut branche geri yükleme:
```bash
git stash apply
```
 
İstenilen saklanma yerini mevcut branche geri yükleme:
*	{stash_number} git stash list ile elde edilebilir
```bash
git stash apply stash@{stash_number}
```
 
Saklanan değişiklikleri kaldırma:
```bash
git stash drop
```
________________________________________

## Arama

Bir metni dizindeki bütün dosyalarda aramak:
```bash
git grep "Merhaba"
```

Bir metni herhangi bir sürüm içinde aramak:
```bash
git grep "Merhaba" v2.5
```

Belirli bir kelimeyi içeren commitleri göstermek:
```bash
git log -S "keyword"
```

Belirli bir kelimeyi içeren commitleri göstermek (düzenli ifadeler kullanarak):
```bash
git log -S "keyword" --pickaxe-regex
```

________________________________________

## Commit Geçmişi

Tüm commitleri en yenisinden başlayarak listeler:
```bash
git log
```

Tüm commitleri görüntüler(Sadece commit hash ve commit mesajı görüntülenir.):
```bash
git log --oneline
```

Belli kullanıcıya ait commitleri görüntüler:
```bash
git log --author="username"
```

Belirli bir dosya üzerinde zaman içinde meydana gelen değişiklikleri göstermektedir:
```bash
git log -p <file>
```

<Dosyayı> kimin ne zaman değiştirdiğini gösterir:
```bash
git blame <file>
```

Referans kayıtlarını gösterir:
```bash
git reflog show
```

Referans kayıtlarını siler:
```bash
git reflog delete
```

________________________________________

## Taşı / Yeniden Adlandır

Dosyayı yeniden adlandırmak:
Index.txt'den Index.html'e
```bash
git mv Index.txt Index.html
```

________________________________________

## Branches & Tags
 
Tüm var olan branchleri listeler:
```bash
git branch
```

Ana branchi değiştirir:
```bash
git checkout <branch>
```

Mevcut ana branchte yeni bir branch oluşturur:
```bash
git branch <new-branch>
```

Remote branchte yeni bir izlenen branch oluşturur:
```bash
git branch --track <new-branch> <remote-branch>
```

Yerel branchi siler:
```bash
git branch -d <branch>
```

Güncel commiti etiket ile işaretler:
```bash
git tag <tag-name>
```

HEADi etiket ile işaretler ve bir mesaj eklemek için yazı editörünü açar:
```bash
git tag -a <tag-name>
```

HEADi bir mesaj içermek şartı ile etiketler:
```bash
git tag <tag-name> -am 'message here'
```

Tüm etiketleri listeler:
```bash
git tag
```

Tüm etiketleri mesajları ile listeler (etiket mesajı yoksa bir etiket mesajı yaz):
```bash
git tag -n
```

________________________________________

## Güncelleştirme & Yayınlama

Yapılandırılmış tüm güncel remoteları listeler:
```bash
git remote -v
```

Belirli bir <remote> hakkında bilgileri gösterir:
```bash
git remote show <remote>
 ```

Yeni remote repository oluşturur, <remote> diye isimlendirir:
```bash
git remote add <remote> <url>
 ```

<Remote> da bulunan tüm değişiklikleri indirir, ama ana brachle birleştirmez:
```bash
git fetch <remote>
 ```

Değişiklikleri indirir ve doğrudan ana brache merge/integrate eder:
```bash
git remote pull <remote> <url>
 ```

Tüm ana Branchteki değişiklikleri yerel repositorye ekler:
```bash
git pull origin master
 ```

Remote da bulunan repositorye(depoya), yerel değişiklikleri yayınlar:
```bash
git push remote <remote> <branch>
 ```

Remote da bulunan bir branchi siler:
```bash
git push <remote> :<branch> (since Git v1.5.0)
 ```
ya da
```bash
git push <remote> --delete <branch> (since Git v1.7.0)
 ```

Etiketleri yayınlar:
```bash
git push --tags
 ```
________________________________________

## Merge & Rebase

Seçili HEADinizi istediğiniz <branch>'e merge eder:
```bash
git merge <branch>
```

Seçili HEADinizi şimdiki <branch>'e rebase yapar
Yayınlanan committen sonra rebase yapmayın!
```bash
git rebase <branch>
```

Rebase iptal etmek:
```bash
git rebase --abort
```

Çakışmaları çözümledikten sonra rebase devam etmek:
```bash
git rebase --continue
```

Çakışmaları çözmek için yapılandırılmış birleştirme aracını kullanmak:
```bash
git mergetool
```

Editörünüzü kullanarak çakışmaları çözümledikten sonra dosyayı çözümlenmiş olarak ekleyin:
```bash
git add <resolved-file>
git rm <resolved-file>
```

Commitleri birleştirmek:
```bash
git rebase -i <commit-just-before-first>
```

Bu metni,
pick <commit_id>
pick <commit_id2>
pick <commit_id3>

bu metin ile değiştirin,
pick <commit_id>
squash <commit_id2>
squash <commit_id3>

________________________________________

## Geri Alma

Çalışılan dosyadaki tüm yerel değişiklikleri kaldırır:
```bash
git reset --hard HEAD
```

Evreleme alanı dışındaki tüm dosyaları alır(örnek: son git add'i geri alır):
```bash
git reset HEAD
```

Belli bir dosyadaki yerel değişiklikleri kaldırır:
```bash
git checkout HEAD <file>
```

Silinen dosyayı geri döndürme dosyanın commit loglarının tutuluyor olması ile mümkündür:
```bash
git revert <commit>
```

Belirlediğiniz HEADden bir önceki commite döner ve belirlemiş olduğunuz committe yaptığınız tüm değişiklikleri geri alır:
```bash
git reset --hard <commit>
```

Belirlediğiniz HEADden bir önceki commite döner ve belirlemiş olduğunuz committe yaptığınız tüm değişiklikleri untracked dosyalar arasına alır:
```bash
git reset <commit>
```

Belirlediğiniz HEADden bir önceki commite döner ve yaptığınız tüm değişiklilkleri local commitlerinizi tutarak geri alır:
```bash
git reset --keep <commit>
```

Gitignore'a eklenmeden önce yanlışlıkla kaydedilmiş dosyaları kaldırın:
```bash
git rm -r --cached .
git add .
git commit -m "remove xyz file"
```

________________________________________

# Git-Flow

 ## Index
 
*	Ayarlar
*	Başlarken
*	Özellikler (Features)
*	Bir Yayın Çıkarırken (Release)
*	Hata Giderimleri (Hotfixes)
*	Komutlar (Commands)

________________________________________

## Ayarlar

Git flow'u kullanabilmek için öncelikli olarak git kurulumunun yapılması gerekmektedir. Git flow OSX, Linux ve Windows üzerinde çalıştırılabilir.
OSX Homebrew:
$ brew install git-flow

OSX Macports:
$ port install git-flow

Linux:
$ apt-get install git-flow

Windows (Cygwin):
Git flow kurulumu için wget ve util-linux gerekmektedir.
$ wget -q -O - --no-check-certificate https://github.com/nvie/gitflow/raw/develop/contrib/gitflow-installer.sh | bash

________________________________________

## Başlarken

Git flow, kullanmak istediğiniz projede ayarlarınızı özelleştirmek amacıyla başlatılır (initialize).
Başlangıç (Initialize):

Bu noktada kafanızda dallarınızı (branches) isimlendirme konusuna ilişkin birçok soru işareti oluşacaktır. Bu bağlamda varsayılan (default) değerleri kullanmanız önerilir.
git flow'u kullanmak istediğiniz reponuzdayken:
git flow init
ya da

varsayılan:
git flow init -d
________________________________________

## Özellikler (Features)

Git flow ile yayınlamak üzere olduğunuz projenize ekleyeceğiniz özellikler için yeni dallarda (feature) kodlama yaparsınız. Genel olarak sadece geliştirici repolarında bulunurlar.
Yeni bir özellik eklemesi başlatmak (feature start):
Yeni özelliklerin eklenmesi öncelikle develop dalından (branch) başlar.
git flow feature start MYFEATURE
Bu komut bize develop dalını (branch) temel alan bir özellik dalı (feature) oluşturur. Ve bulunduğumuz dalı develop/MYFEATURE olarak değiştirir.
Bir özellik eklemesi bitirilirken (feature finish):
Bir özelliğin eklenme işlemi bitirilirken şunları yapılır:
1)Kendi çalıştığımız özellik dalı (burada MYFEATURE) develop ana dalı ile birleştirilir.
2)Bu birleşmeden sonra kendi özellik dalımız (MYFEATURE) silinir.
3)Bulunduğumuz dal tekrar develop olarak değiştirilir.
git flow feature finish MYFEATURE
Bir özelliği yayınlamak (Publish a feature):
Bir ekip içerisinde geliştirme mi yapıyorsunuz? O zaman geliştirdiğiniz özelliği bir uzak sunucuya gönderin, böylelikle geliştirdiğiniz özellik diğer kullanıcılar tarafından kullanılabilir.
git flow feature publish MYFEATURE
Yayınlanmış bir özelliği almak (Getting a published feature):
Uzak sunucu üzerinde yayınlanmış bir özelliği kendi yerel (local) çalışma ortamınıza aktarırken:
git flow feature pull origin MYFEATURE
________________________________________
Bir Yayın Çıkarırken (Release)
Yeni bir ürünün yayınlanmasına yardımcı olur. Küçük hata giderimleri ve meta-data hazırlığı için kullanılabilir.
Bir sürüm yayınlamak (Start a release):
Bu komut ile develop dalını temel kabul eden bir release dalı (branch) yaratılır.
Opsiyonel olarak yayınınızın [BASE] noktasından başlamasını sağlayabilirsiniz. Bu commit develop dalında (branch) iken yapılmalıdır.
git flow release start RELEASE [BASE]
Yayınlama dalınız (release branch) oluştuktan sonra bu yöntem ile diğer yazılımcılar tarafından yapılan release commitlerinin de kabul edilmesini sağlayabilirsiniz. Bunu özellik yayınlama (feature publishing) ile kolaylıkla yapabilirsiniz.
git flow release publish RELEASE
(Uzak sunucu üzerindeki yayınları git flow release track RELEASE ile izleyebilirsiniz. )
Bir sürüm yayınını tamamlamak(Finish up a release):
Bir sürüm yayınını tamamlarken git dallanmasının (branching) en büyük adımını atarız. Yayınlanma tamamlanırken:
1)Yayınlama yaptığımız dal olan release dalı (branch) master ana dalı ile birleştirilir.
2)Etiketler (tags) isimleri ile birlikte yayınlanır.
3)Arkaplandaki birleştirmeler (back-merges) develop dalında yayınlanır.
4)Yayınlama için açmış olduğumuz dal (branch) silinir.
git flow release finish RELEASE
Ancak etiketlerinizi de eklemeyi unutmayın! git push --tags bu sorununuzu da halledecektir.
________________________________________
Hata giderimleri (Hotfixes)
Yayına çıkarılmış bir versiyonda istenmeyen durumlar ortaya çıktığında ani hata giderimi için kullanılır. Hotfixler, master ana dalı (branch)ındaki versiyon numarasını belirten etiketten dallanır (branching).
Bir hata giderimini başlatmak(git flow hotfix start):
Diğer git flow komutlarında olduğu gibi bir hotfix başlatılırken:
$ git flow hotfix start VERSION [BASENAME]
Versiyon argümanları yeni hotfix yayınının adını alır. Opsiyonel olarak başlangıç noktası için bir isim özelleştirmesi yapabilirsiniz (basename).
Hata giderimi bitirme (Finish a hotfix):
Bir hata giderimi tamamlanırken, develop ve master dalları ile birleştirilir. Ayrıca master dalına (branch) hotfix versiyonunun etiketi eklenir.
git flow hotfix finish VERSION

