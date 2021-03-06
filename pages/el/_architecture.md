
# Αρχιτεκτονική

Η δόμηση ενός CSS project είναι ίσως ένα απο τα δυσκολότερα πράγματα που θα κάνετε κατα την διαρκεια ζωής του project. Το να συντηρήσετε την δόμηση αυτή συνεπή και ουσιώδης είναι ακόμα δυσκολότερο.

Ευτυχώς, ένα απο τα βασικά πλεονεκτήματα της χρήσης ενός CSS preprocessor είναι η παροχή της δυνατότητας τμηματοποίησης του κώδικα σε πολλά αρχεία χωρίς να επηρεάζεται η απόδοση του (όπως με το `@import` CSS directive). Λόγο της υπερφόρτωσης που κάνει η Sass στο `@import` directive, είναι απολύτως ασφαλή (και συνιστάται ανεπιφύλακτα) η χρήση όσο αρχείων χρειάζεται κατα την διάρκεια της ανάπτυξης, αφού όλα τα αρχεία θα συγκεντρωθούν σε ένα αρχείο CSS σε production περιβάλλον.

Πέρα από αυτό, δεν μπορώ να τονίσω αρκετά την ανάγκη για χρήση φακέλων, ακόμα και σε μικρά projects. Στο σπίτι, δεν πετάς όλα τα χαρτιά στο ίδιο κουτί. Χρησιμοποιείς φακέλους, εναν για το σπίτι/διαμέρισμα, έναν για την τράπεζα, έναν για τους λογαριασμούς και τα λοιπά. Δεν υπάρχει λόγος να γίνει διαφορετικά και για την δόμηση του CSS project σας. Διαχωρίστε τον κώδικα σε διαφορετικούς φακέλους, ονομασμένους λογικά, έτσι ώστε αργότερα να σας είναι εύκολο να βρείτε αυτό που ψάχνετε εύκολα και γρήγορα.

Υπάρχουν πολλές δημοφιλείς [αρχιτεκτονικές](https://www.sitepoint.com/look-different-sass-architectures/) για CSS project(s) όπως: [OOCSS](https://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/), [Atomic Design](https://bradfrost.com/blog/post/atomic-web-design/), projects βασισμένα σε [Bootstrap](https://getbootstrap.com/) ή σε [Foundation](https://get.foundation/)… Τα οποία έχουν πλεονεκτήματα και μειονεκτήματα.

Εγώ, προσωπικά, χρησιμοποιώ μια προσέγγιση που μοιάζει πολύ με αυτή του [SMACSS](http://smacss.com/) του [Jonathan Snook](https://snook.ca/), η οποία επικεντρώνεται στην διατήρηση της κατάστασης όσο πιο απλής και φανερής γίνεται.

<div class="note">
  <p>Έχω μάθει πως η δόμηση του κώδικα τις περισσότερες φορές αλλάζει ανάλογα με το project. Μη διστάσετε να απορρίψετε εντελώς ή να προσαρμόσετε την προτεινόμενη λύση έτσι ώστε να φτάσετε σε ένα αποτέλεσμα που θα ταιριάζει στις ανάγκες σας.</p>
</div>

## Components

Υπάρχει μια τεράστια διαφορά μεταξύ του να κάνεις κάτι *να δουλεύει* και να κάνει κάτι *καλά*. Πάλι, η CSS είναι πολύ «ακατάστατη» γλώσσα <sup>[citation needed]</sup>. Όσο λιγότερη CSS έχουμε, τόσο το καλύτερο. Δεν θέλουμε να αντιμετωπίσουμε καταστάσεις στις οποίες θα έχουμε megabytes απο κώδικα CSS. Για να κρατήσουμε τα stylesheets μικρά και αποδοτικά &mdash;&thinsp;και προφανώς δεν θα σας ξαφνιάσει&thinsp;&mdash; είναι καλό να σκεφτόμαστε το interface ως μια συλλογή απο components.

Τα Components μπορεί να είναι οτιδήποτε, αρκεί:

* να κάνουν μόνο ένα πράγμα·
* να είναι επαναχρησιμοποιήσιμα και να επαναχρησιμοποιούνται μέσα στο project·
* να είναι ανεξάρτητα.

Για παράδειγμα, μια φόρμα αναζήτησης θα πρέπει να θεωρείται ως ένα component. Πρέπει να είναι επαναχρησιμοποιήσιμο, σε διαφορετικές τοποθεσίες, σε διαφορετικές σελίδες, σε διαφορετικές καταστάσεις. Δεν πρέπει να εξαρτάται απο την θέση του στο DOM (footer, sidebar, κύριο περιεχόμενο…).

Σχεδόν όλα τα interface μπορούμε να τα θεωρήσουμε ως components και είναι αυτό που σας συνιστώ. Αυτό θα μικρύνει κατά πολύ την ποσότητα CSS κώδικα που χρειάζεται το project, αλλά τυγχάνει επίσης να είναι και ευκολότερο στην συντήρηση από ένα χάος όπου όλα είναι ακατάστατα.

## Δομή Component

Ιδανικά, τα components πρέπει να βρίσκονται μέσα σε δικά τους Sass partial (μέσα στον φάκελο `components/`, όπως περιγράφεται στο [7-1 pattern](#pattern)), π.χ. `components/_button.scss`. Τα styles που περιγράφονται μέσα σε κάθε αρχείο component πρέπει να έχουν να κάνουν μόνο με:

* Το style του ίδιου του component·
* Το style παραλλαγών, τροποποιητών ή/και καταστάσεων του component·
* Τα styles των απογόνων του component (λ.χ. children), εάν είναι απαραίτητο.

Αν θέλετε τα components σας να παίρνουν το θέμα τους απο εξωτερικούς παράγοντες (π.χ. απο ένα θέμα μέσα στο φάκελο `themes/`), περιορίστε τις δηλώσεις σας σε δομικά styles, όπως είναι οι διαστάσεις (width/height), padding, margins, alignment, και τα λοιπά. Αποκλείστε styles όπως τα χρώματα, σκιές, font rules, background rules, και τα λοιπά.

Ένα component partial μπορεί να περιέχει παραλλαγές σχετικές με το component, placeholders, ακόμα και mixins ή functions. Κρατήστε στο μυαλό σας, όμως, ότι πρέπει να αποφύγετε το referencing (π.χ. να κάνετε `@import`) component αρχεία μέσα απο άλλα αρχεία component, γιατί αυτό μπορεί να κάνει το dependency graph του project σας αδύνατο να συντηρηθεί.

Εδώ είναι ένα παράδειγμα component partial ενός button:

{% include snippets/architecture/06/index.html %}

<div class="note">
  <p>Ευχαριστώ τον <a href="https://twitter.com/davidkpiano">David Khourshid</a> για τη βοήθεια και την εμπειρογνωμοσύνη που προσέφερε σε αυτό το τμήμα.</p>
</div>

## Το 7-1 pattern

Επιστρέφουμε στην αρχιτεκτονική. Συνηθίζω να ακολουθώ το *7-1 pattern*: 7 φακέλους, 1 αρχείο. Ουσιαστικά, έχεις όλα τα partials μέσα σε 7 διαφορετικούς φακέλους, και ένα αρχείο στο πρώτο επίπεδο (συνήθως με την ονομασία `main.scss`) το οποίο κάνει import όλα τα άλλα για να τα κάνει compile σε ένα CSS stylesheet.

* `base/`
* `components/`
* `layout/`
* `pages/`
* `themes/`
* `abstracts/`
* `vendors/`

Και φυσικά:

* `main.scss`

<div class="note">
  <p>Αν σας ενδιαφέρει να χρησιμοποιήσετε το 7-1 pattern, υπάρχει ήδη το <a href="https://github.com/KittyGiraudel/sass-boilerplate">boilerplate</a> έτοιμο στο GitHub. Πρέπει να περιέχει όλα όσα χρειάζεστε για να ξεκινήσετε με αυτή την αρχιτεκτονική.</p>
</div>

{% include images/wallpaper.html %}

Ιδανικά, μπορούμε να καταλήξουμε σε κάτι σαν αυτό:

{% include snippets/architecture/01/index.html %}

<div class="note">
  <p>Τα αρχεία ακολουθούν την ίδια ονοματική σύμβαση που περιγράψαμε παραπάνω: είναι οριοθετημένα με κάτω παύλα.</p>
</div>

### Φάκελος Base

O φάκελος `base/` περιέχει αυτό που αποκαλούμε κώδικα boilerplate για το project. Εκεί μπορεί να βρεθεί το reset αρχείο, κάποια τυπογραφικά rules, και πιθανότητα ένα stylesheet (το οποίο συνηθίζω να αποκαλώ `_base.scss`), στο οποίο ορίζω διάφορα standard στύλ για HTML elements που χρησιμοποιούνται συνήθως.

* `_base.scss`
* `_reset.scss`
* `_typography.scss`

<div class="note">
  <p>Αν το project σας χρησιμοποιεί <em>πολλά</em> CSS animations, ίσως πρέπει να σκεφτείτε την προσθήκη του αρχείου <code>\_animations.scss</code> μέσα το οποίο θα περιέχει τους <code>@keyframes</code> ορισμούς απο όλα τα animations σας. Εάν τα χρησιμοποιείτε περιστασιακά, αφήστε τα να βρίσκονται μαζί τους selectors που τα χρησιμοποιούν.</p>
</div>

### Φάκελος Layout

Ο φάκελος `layout/` περιέχει όλα όσα έχουν να κάνουν με την δομή του site ή την εφαρμογής. Αυτός ο φάκελος μπορεί να περιέχει stylesheets για τα βασικά κομμάτια του site (header, footer, navigation, sidebar…), το grid system ή ακόμα και CSS styles για όλα τα forms.

* `_grid.scss`
* `_header.scss`
* `_footer.scss`
* `_sidebar.scss`
* `_forms.scss`
* `_navigation.scss`

<div class="note">
  <p>Ο <code>layout/</code> φάκελος θα μπορούσε επίσης να ονομαστεί <code>partials/</code>, αναλόγως τι προτιμάτε.</p>
</div>

### Φάκελος Components

Για μικρότερα components, υπάρχει ο φάκελος `components/`. Ενώ ο φάκελος `layout/` είναι *macro* (καθορίζει το γενικό μοντέλο της σελίδας), ο φάκελος `components/` είναι επικεντρωμένος στα widgets. Περιέχει modules ολών των ειδών όπως slider, loader, widget, και οτιδήποτε άλλο προς αυτή την κατεύθυνση. Συνήθως υπάρχουν πολλά αρχεία μέσα στον φάκελο `components/` αφού όλο το site ή η εφαρμογή απαρτίζεται απο μικρά modules.

* `_media.scss`
* `_carousel.scss`
* `_thumbnails.scss`

<div class="note">
  <p>Ο φάκελος <code>components/</code> θα μπορούσε επίσης να ονομαστεί <code>modules/</code>, αναλόγος τι προτιμάται.</p>
</div>

### Φάκελος Pages

Αν έχετε στυλιστικό κώδικα μόνο για συγκεκριμένες σελίδες, είναι προτιμότερο να μπούν στον φάκελο `pages/`, σε ένα αρχείο που παίρνει το ονομά του από την σελίδα. Για παράδειγμα, δεν είναι ασυνήθιστο το να έχεις στυλιστικό κώδικα για την αρχική σελίδα εξού και η ανάγκη για ένα `_home.scss` αρχείο μέσα στον φάκελο `pages/`.

* `_home.scss`
* `_contact.scss`

<div class="note">
  <p>Ανάλογα με τη διαδικασία deployment σας, αυτά τα αρχεία θα μπορούσαν να χρησιμοποιηθούν απο μόνα τους για να να αποφευχθεί η συγχώνευσή τους στο τελικό stylesheet. Είναι πραγματικά στο χέρι σας.</p>
</div>

### Φάκελος Themes

Σε μεγάλα sites και εφαρμογές, δεν είναι ασυνήθιστο το να έχεις διαφορετικά θέματα. Υπάρχουν πάρα πολλοί τρόποι για να αντιμετώπισης το θεμα αυτό αλλά προσωπικά προτιμό να τα έχω όλα μέσα στον φάκελο `themes/`.

* `_theme.scss`
* `_admin.scss`

<div class="note">
  <p>Αυτό είναι πολύ συγκεκριμένο στο project και είναι πολύ σπάνιο να υπάρχει σε άλλα projects αφού τα περισσότερα μεγάλα sites και εφαρμογές έχουν διαφορετικές απαιτήσεις και αρχιτεκτονική.</p>
</div>

### Φάκελος Abstracts

Ο Φάκελος `abstracts/` συγκεντρώνει όλα τα Sass tools και helpers που χρησιμοποιούνται σε όλο το project. Κάθε global μεταβλητή, συνάρτηση, mixin και placeholder πρέπει να μπει εκεί.

O γενικός κανόνας του φακέλου αυτού είναι ότι δεν πρέπει να παράγεται ούτε μια γραμμή CSS όταν γίνει compile μόνος του γιατί απλά αποτελείται από Sass helpers.

* `_variables.scss`
* `_mixins.scss`
* `_functions.scss`
* `_placeholders.scss`

Όταν δουλεύεις σε ένα πολύ μεγάλο project με πολλά αφηρημένα utilities, θα μπορούσες να τα ομαδοποιήσεις ανάλογα με το θέμα τους αντί για τον τύπο τους, για παράδειγμα τυπογραφία (`_typography.scss`), theming (`_theming.scss`), κτλ. Κάθε αρχείο περιέχει όλα τα σχετικά helpers: μεταβλητές, functions, mixins και placeholders. Με αυτόν τον τρόπο ο κώδικας μπορεί να γίνει πιο εύκολος στην ανάγνωση και την συντήρηση, ειδικά όταν τα αρχεία γίνονται πολύ μεγάλα.

<div class="note">
  <p>Ο φάκελος <code>abstracts/</code> θα μπορούσε επίσης να ονομαστεί <code>utilities/</code> ή <code>helpers/</code>, αναλόγως τι προτιμάς.</p>
</div>

### Φάκελος Vendors

Και τελευταίο αλλά εξίσου σημαντικό, τα περισσότερα projects θα έχουν έναν `vendors/` φάκελο ο οποίος περιέχει όλα τα CSS αρχεία από εξωτερικές βιβλιοθήκες όπως Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, και ούτω καθεξής. Βάζοντας τα σε αυτόν τον φάκελο είναι ένας καλός τρόπος για να πείς “Αυτός δεν είναι δικός μου κώδικας, δεν είναι δικιά μου ευθύνη”.

* `_normalize.scss`
* `_bootstrap.scss`
* `_jquery-ui.scss`
* `_select2.scss`

Αν θέλετε να παρακάμψετε τμήμα κάποιου vendor, προτείνω να φτιάξετε έναν όγδοο φάκελο με όνομα `vendors-extensions/` στο οποίο μπορείς να βάλεις αρχεία που έχουν το ίδιο όνομα με το αρχείο που θες να παρακάμψεις απο τον φάκελο vendors.

Για παράδειγμα, `vendors-extensions/_boostrap.scss` είναι ένα αρχείο που περιέχει όλα τα CSS rules που αποσκοπούν στην εκ νέου δηλώση κάποιων απο τις προεπιλεγμένες του Bootstrap. Έτσι δεν χρειάζεται να να πειράξεις απευθείας τα vendor αρχεία, το οποίο γενικά δεν είναι καλή ιδέα.

### Το αρχείο Main

Το αρχείο main (το οποίο συνήθως ονομάζεται `main.scss`) πρέπει να είναι το μόνο Sass αρχείο απο το ολόκληρο το code base του οποίου το όνομα δεν ξεκινάει απο τον χαρακτήρα της κάτω παύλας. Το αρχείο αυτό δεν πρέπει να περιέχει τίποτα εκτός απο γραμμές `@import` και σχολίων.

Τα αρχεία πρέπει να γίνονται import με βάση τον φάκελο στον οποίο βρίσκονται, το ένα μετά το άλλο με την ακόλουθη σειρά:

1. `abstracts/`
1. `vendors/`
1. `base/`
1. `layout/`
1. `components/`
1. `pages/`
1. `themes/`

Προκειμένου να διατηρηθεί η αναγνωσιμότητα, το αρχείο main θα πρέπει να ακολουθεί τις παρακάτω κατευθυντήριες γραμμές:

* ένα αρχείο ανα `@import`·
* ενα `@import` ανα γραμμή·
* καμία κενή γραμμή μεταξύ δύο import απο τον ίδιο φάκελο·
* μια κενή γραμμή μετά απο το τελευταίο import ενός φακέλου·
* οι επεκτάσεις των αρχείων και οι χαρακτήρες κάτω παύλας που προηγούνται πρέπει να παραλειφθούν.

{% include snippets/architecture/02/index.html %}

Υπάρχει ακόμα ένας τρόπος για να κάνεις import partial αρχεία τον οποίο θεωρώ έγκυρο. Στη θετική πλευρά, κάνει τα αρχεία ευανάγνωστα. Απο την άλλη, τα κάνει δυσκολότερα στην ενημέρωση. Εν πάση περιπτώσει, θα αφήσω εσάς να αποφασίσετε ποια είναι η καλύτερη, δεν έχει πολύ σημασία. Για αυτόν τον τρόπο, το αρχείο main θα πρέπει να τηρεί τις ακόλουθες κατευθυντήριες γραμμές:

* ένα `@import` ανά φάκελο·
* ένα linebreak ανά `@import`·
* κάθε αρχεία σε δικιά του γραμμή·
* μια κενή γραμμή μετά το τελευταίο import ενός φακέλου·
* οι επεκτάσεις των αρχείων και οι χαρακτήρες κάτω παύλας που προηγούνται πρέπει να παραλειφθούν.

{% include snippets/architecture/03/index.html %}

## Σχετικά με το globbing

Στον προγραμματισμό ηλεκτρονικών υπολογιστών, τα glob patterns καθορίζουν σύνολα ονομάτων αρχείων με χαρακτήρες μπαλαντέρ, όπως `*.scss`. Γενικά, το globbing είναι η επιλογή ενός σύνολο αρχείων βασιζόμενη σε ένα expression αντί κάποιας λίστας ονομάτων αρχείων.
Όταν εφαρμόζεται στη Sass, σημαίνει το import partial αρχείων μέσα στο [αρχείο main](#main) με ένα glob pattern αντί του να τα απαριθμήσουμε μεμονωμένα. Αυτό θα έκανε το αρχείο main να μοιάζει κάπως έτσι:

{% include snippets/architecture/05/index.html %}

Η Sass δεν υποστηρίζει το file globbing απο μόνο του γιατί μπορεί να είναι μια επικίνδυνη λειτουργία γιατί στη CSS υπάρχει προτεραιότητα στην σειρά των δηλώσεων. Όταν κάνουμε import αρχείων δυναμικά (το οποίο συνήθως γίνεται με αλφαβητική σειρά), χάνεται ο έλεγχος της σειράς προτεραιότητας, κάτι που μπορεί να οδηγήσει σε παρενέργειες.

Κατόπιν αυτού, σε μια αυστηρή component-based αρχιτεκτονική με επιπλέον προσοχή προσοχή στο να μη διαρρεύσει κανένα style από ένα partial στο άλλο, η σειρά δεν θα 'πρεπε να έχει σημασία πια, κάτι το οποίο θα επέτρεπε τα glob imports. Αυτό θα καθιστούσε ευκολότερη την πρόσθεση ή αφαίρεση partials, μιας και δεν θα ήταν πλέον απαραίτητη η προσεκτική ενημέρωση του αρχείου main.

Για τη χρήση Ruby Sass, υπάρχει ένα Ruby gem που ονομάζεται [sass-globbing](https://github.com/chriseppstein/sass-globbing) που επιτρέπει ακριβώς αυτή τη συμπεριφορά. Αν όμως χρησιμοποιείτε node-sass, μπορείτε να βασιστείτε είτε στο Node.js, είτε σε οποιοδήποτε build tool χρησιμοποιείτε για να κάνετε το compilation (Gulp, Grunt, etc.).

## Το αρχείο Shame

Υπάρχει μια ενδιαφέρουσα ιδέα που έχει γίνει δημοφιλής απο τους [Harry Roberts](https://csswizardry.com), [Dave Rupert](https://daverupert.com) και [Chris Coyier](https://css-tricks.com) η οποία συνιστά να βάζουμε όλα τα CSS declarations, hacks και πράγματα για τα οποία δεν είμαστε περήφανοι μέσα στο [αρχείο *shame*](https://csswizardry.com/2013/04/shame-css-full-net-interview/). Αυτό το αρχείο, με τον δραματικό τίτλο `_shame.scss`, θα γινόταν import μετά από όλα τα άλλα αρχεία στο τέλος του stylesheet.

{% include snippets/architecture/04/index.html %}
