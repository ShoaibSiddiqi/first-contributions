window._bc = window._bc || {};

window._bc.addHidden = function (form, name, value) {
    var elements = document.getElementsByName(name);
    var input = null;
    if (elements.length > 0) {
        for (var i = 0; i < elements.length; i++) {
            var typeAttr = elements[i].attributes['type'];
            if (typeof typeAttr !== 'undefined' && typeAttr.value === 'hidden') {
                input = $(elements[i]);
                break;
            }
        }
    }

    if (input === null) {
        input = $('<input type="hidden" />');
        input.attr('name', name);
        input.val(value);
        form.append(input);
    } else {
        input.val(value);
    }

    return input;
};

window._bc.addHiddenObject = function(form, object, prefix) {
    prefix = prefix || '';
    if (_bc.isArray(object)) {
        object.forEach(function (val, i) {
            window._bc.addHiddenObject(form, val, prefix + '[' + i + '].');
        });
    } else if (_bc.isObject(object)) {
        for (var prop in object) {
            if (object.hasOwnProperty(prop)) {
                window._bc.addHiddenObject(form, object[prop], prefix + prop);
            }
        }
    } else if (typeof (object) !== 'undefined' && object !== null) {
        window._bc.addHidden(form, prefix, object);
    }
};

window._bc.isObject = function (val) {
    if (val === null) { return false; }
    return ((typeof val === 'function') || (typeof val === 'object'));
};

window._bc.isArray = function(value) {
    // Use compiler's own isArray when available
    if (Array.isArray) {
        return Array.isArray(value);
    }

    var objectToStringFn = Object.prototype.toString,
        arrayToStringResult = objectToStringFn.call([]);

    return objectToStringFn.call(value) === arrayToStringResult;
};

window._bc.isValidEmail = function (email) {
    var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(String(email).toLowerCase());
};

window._bc.validateForm = function (form) {
    var isValid = true;

    form.find('input[required]').each(function (i, val) {
        var $val = $(val);
        var next = $val.next('span.form-error');
        if (next) {
            var validity = val.validity.valid;

            if ($val.prop('type') === 'email') {
                validity = window._bc.isValidEmail($val.val());
            }

            if (!validity) {
                next.addClass('is-visible');
                isValid = false;
            }
            else {
                next.removeClass('is-visible');
            }
        }
    });

    return isValid;
};

window._bc.isBot = function () {
    var botPattern = "(googlebot\/|Googlebot-Mobile|Googlebot|Googlebot-Image|Google favicon|Mediapartners-Google|bingbot|slurp|java|wget|curl|Commons-HttpClient|Python-urllib|libwww|httpunit|nutch|phpcrawl|msnbot|jyxobot|FAST-WebCrawler|FAST Enterprise Crawler|biglotron|teoma|convera|seekbot|gigablast|exabot|ngbot|ia_archiver|GingerCrawler|webmon |httrack|webcrawler|grub.org|UsineNouvelleCrawler|antibot|netresearchserver|speedy|fluffy|bibnum.bnf|findlink|msrbot|panscient|yacybot|AISearchBot|IOI|ips-agent|tagoobot|MJ12bot|dotbot|woriobot|yanga|buzzbot|mlbot|yandexbot|purebot|Linguee Bot|Voyager|CyberPatrol|voilabot|baiduspider|citeseerxbot|spbot|twengabot|postrank|turnitinbot|scribdbot|page2rss|sitebot|linkdex|Adidxbot|blekkobot|ezooms|dotbot|Mail.RU_Bot|discobot|heritrix|findthatfile|europarchive.org|NerdByNature.Bot|sistrix crawler|ahrefsbot|Aboundex|domaincrawler|wbsearchbot|summify|ccbot|edisterbot|seznambot|ec2linkfinder|gslfbot|aihitbot|intelium_bot|facebookexternalhit|yeti|RetrevoPageAnalyzer|lb-spider|sogou|lssbot|careerbot|wotbox|wocbot|ichiro|DuckDuckBot|lssrocketcrawler|drupact|webcompanycrawler|acoonbot|openindexspider|gnam gnam spider|web-archive-net.com.bot|backlinkcrawler|coccoc|integromedb|content crawler spider|toplistbot|seokicks-robot|it2media-domain-crawler|ip-web-crawler.com|siteexplorer.info|elisabot|proximic|changedetection|blexbot|arabot|WeSEE:Search|niki-bot|CrystalSemanticsBot|rogerbot|360Spider|psbot|InterfaxScanBot|Lipperhey SEO Service|CC Metadata Scaper|g00g1e.net|GrapeshotCrawler|urlappendbot|brainobot|fr-crawler|binlar|SimpleCrawler|Livelapbot|Twitterbot|cXensebot|smtbot|bnf.fr_bot|A6-Indexer|ADmantX|Facebot|Twitterbot|OrangeBot|memorybot|AdvBot|MegaIndex|SemanticScholarBot|ltx71|nerdybot|xovibot|BUbiNG|Qwantify|archive.org_bot|Applebot|TweetmemeBot|crawler4j|findxbot|SemrushBot|yoozBot|lipperhey|y!j-asr|Domain Re-Animator Bot|AddThis)";
    var expression = new RegExp(botPattern, 'i');
    return expression.test(navigator.userAgent);
};

/* Shortlist functionality */
(function () {
    var SHORTLIST_ATTRIBUTE = '[data-shortlist]';
    function ShortList() {
        this.isToggled = false;
        this.length = 0;
        this.element = $('.shortlist');
        var _toggles = $(SHORTLIST_ATTRIBUTE).parent();

        var __constructor = function (self) {
            _toggles
                .on('click', _toggleShortlist);
        }(this);
    };

    // Show the shortlist panel
    ShortList.prototype.show = function () {
        if (!_isExpanded(this.element)) {
            this.isToggled = true;
            this.element.foundation('toggle');
        }
    }

    function _isExpanded($element) {
        return $element.attr('aria-expanded') === 'true';
    }

    function _toggleShortlist(e) {
        $(e.currentTarget)
            .find(SHORTLIST_ATTRIBUTE)
            .foundation('toggle');
    }

    //window._bc.ShortList.prototype.toggle = function () {
    //    this.shortlistToggled = true;
    //    this._shortlist.foundation('toggle');
    //};

    //function _removeFavourite(e) {
    //    toggleFavourite(e).then(function (data) {
    //        shortlistCount--;
    //        if (shortlistCount <= 0 && shortlistToggled) {
    //            shortlistToggled = false;
    //            $shortlist.foundation('toggle');
    //        }
    //    });
    //}

    //window._bc.ShortList.prototype.toggleFavourite = function (e) {
    //    var self = this;
    //    var $target = $(e.target);
    //    var token = $target.attr('data-shortlist');

    //    //Disable the shortlist click while doing the request
    //    self._toggles.off('click', _toggleShortlist);

    //    return new Promise(function (resolve, reject) {
    //        $.post('/maker/logo/' + token + '/favourite',
    //            function (data) {
    //                self._toggles.on('click', _toggleShortlist);

    //                updateTile(token, data);

    //                replaceState(token, data);

    //                resolve();
    //            });
    //    });
    //    };



    //    function _restoreFromState() {
    //        if (window.history && window.history.state) {
    //            var data = window.history.state;

    //            $(data).each(function (i, val) {
    //                updateTile(val.token, val.token ? null : val);
    //                if (val.token) {
    //                    $('i[data-shortlist=' + val.token + ']').removeClass('is-shortlisted');
    //                } else {
    //                    $('i[data-shortlist=' + val.LogoToken + ']').addClass('is-shortlisted');
    //                }
    //            });

    //            shortlistCount = $('#panel-shortlist [data-shortlist]').length;
    //            shortlistToggled = shortlistCount > 0;
    //        }
    //    }

    window._bc.ShortList = ShortList;
})();

window._bc.fadeInElementWithDelay = function ($element, delay, opacityDelay) {
    setTimeout(function () {
        $element.animate({ opacity: 1 }, !isNaN(opacityDelay) ? delay : 1000);
    }, !isNaN(delay) ? delay : 5000);
}

window._bc.fadeOutElementWithDelay = function ($element, delay, opacityDelay) {
    setTimeout(function () {
        $element.animate({ opacity: 0 }, !isNaN(opacityDelay) ? delay : 1000);
    }, !isNaN(delay) ? delay : 5000);
}
