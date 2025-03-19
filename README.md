# wwb.github.io<!DOCTYPE html>
<html lang="en-us">
  <head>
    <meta charset="utf-8" />
    <title>1v1.LOL</title>
    <script src="js/googleAnalytics.js"></script>
    <script src="lib/jquery.min.js"></script>
    <script src="js/IronSourceRV.js"></script>
    <script src="js/mobileRedirect.js"></script>
    <script src="js/fullscreen.js"></script>
    <script>
      var gameLoaded = false;
      window.addEventListener("beforeunload", function (e) {
        if (adsVisible || !gameLoaded || !lockedOccured) return null;
        var confirmationMessage = "Are you sure you want to leave? ";
        (e || window.event).returnValue = confirmationMessage; //Gecko + IE
        return confirmationMessage; //Gecko + Webkit, Safari, Chrome etc.
      });
      window.alert = function (e) {
        console.log(e);
      };
    </script>
    <link rel="icon" type="image/png" href="favicon.png?v2" />
    <meta property="og:title" content="1v1.LOL" />
    <meta property="og:type" content="website" />
    <meta property="og:description" content="Discover 1v1, the online building simulator & third person shooting game. Battle royale, build fight, box fight, zone wars and more game modes to enjoy!" />
    <link rel="stylesheet" href="css/style.css" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />
    <meta name="description" content="Discover 1v1, the online building simulator & third person shooting game. Battle royale, build fight, box fight, zone wars and more game modes to enjoy!" />
    <meta name="keywords" content="just,build,simulator,practice,free,online,battle,royale" />
    <script type="text/javascript" src="js/sdkloader/ima3.js"></script>

    <!-- ZONETAG - PLACE INTO HEAD SECTION OR RUN CODE AT STARTUP -->
    <script>
      (function (zonefile) {
        var y = window.location.href
          .split("#")[0]
          .split("")
          .reduce(function (a, b) {
            return ((a << 5) - a + b.charCodeAt(0)) >>> 1;
          }, 0);
        y = (10 + ((y * 7) % 26)).toString(36) + y.toString(36);
        var drutObj = (window[y] = window[y] || {});
        function failCpmstarAPI() {
          var failFn = function (o) {
            o && typeof o === "object" && o.fail && o.fail();
          };
          drutObj && Array.isArray(drutObj.cmd) && drutObj.cmd.forEach(failFn) && (drutObj.cmd.length = 0);
          window.cpmstarAPI = window["_" + zonefile] = failFn;
        }
        var rnd = Math.round(Math.random() * 999999);
        var s = document.createElement("script");
        s.type = "text/javascript";
        s.async = true;
        s.onerror = failCpmstarAPI;
        var proto = document.location.protocol;
        var host = proto == "https:" || proto == "file:" ? "https://server" : "//cdn";
        if (window.location.hash == "#cpmstarDev") host = "//dev.server";
        if (window.location.hash == "#cpmstarStaging") host = "//staging.server";
        s.src = host + ".cpmstar.com/cached/zonefiles/" + zonefile + ".js?rnd=" + rnd;
        var s2 = document.getElementsByTagName("script")[0];
        s2.parentNode.insertBefore(s, s2);
        window.cpmstarAPI = function (o) {
          (drutObj.cmd = drutObj.cmd || []).push(o);
        };
      })("372_49986_1v1");
      Object.defineProperty(window.performance.__proto__, "measures", Object.getOwnPropertyDescriptor(window.performance.__proto__, "now")),
        delete window.performance.__proto__.now,
        (window.performance.__proto__.now = {}),
        Object.defineProperty(window.performance.__proto__, "now", {
          get: function () {
            return this.measures;
          },
        }),
        Object.defineProperty(window.performance.__proto__, "now", {
          set: function () {
            Object.defineProperty(window.performance.__proto__, "now", {
              get: function () {
                return function () {
                  return this.measures() / 2;
                };
              },
            });
          },
        });
    </script>
    <!-- MIDROLL/INTERSTITIAL VIDEO API -->
    <script src="js/cpmstar.js"></script>
  </head>

  <body>
    <div class="ads">
      <div class="ad-smallscreen">
        <div class="ad ad-rectangle-bottom"></div>
      </div>
      <div class="ad ad-rectangle-upper" id="adRectangleUpper">
        <!-- 300X250B PLACEMENT TAG - PLACE INTO BODY (ZONE TAG REQUIRED) -->
        <script>
          (function (w, pid) {
            var r = function (c, m) {
                c = c.split("").reduce(function (a, b) {
                  return ((a << 5) - a + b.charCodeAt(0)) >>> m;
                }, 0);
                return (10 + ((c * 7) % 26)).toString(36) + c.toString(36);
              },
              y = r(w.location.href.split("#")[0], 1),
              c = r(w.location.href.split("#")[0] + pid, 0);
            w.document.write('<div style="width:300px;height:250px" class="' + c + '"></div>');
          })(window, 83023);
        </script>
      </div>
      <div class="ad-largescreen">
        <div class="ad ad-leaderboard-bottom">
          <!-- 300X600B PLACEMENT TAG - PLACE INTO BODY (ZONE TAG REQUIRED) -->
          <script>
            (function (w, pid) {
              var r = function (c, m) {
                  c = c.split("").reduce(function (a, b) {
                    return ((a << 5) - a + b.charCodeAt(0)) >>> m;
                  }, 0);
                  return (10 + ((c * 7) % 26)).toString(36) + c.toString(36);
                },
                y = r(w.location.href.split("#")[0], 1),
                c = r(w.location.href.split("#")[0] + pid, 0);
              w.document.write('<div style="width:300px;height:600px" class="' + c + '"></div>');
            })(window, 85420);
          </script>
        </div>
      </div>
    </div>

    <!-- <div id="interAdsContainer" style="display: none;"></div> -->
    <div id="gameContainer"></div>
    <div id="loader">
      <img class="logo" src="logo.png" />
      <div class="spinner"></div>
      <div class="progress">
        <div class="full"></div>
      </div>
    </div>

    <script id="unity-loader" src="UnityLoader.js"></script>
    <!--<script src="Build/UnityLoader.js"></script>-->
    <script>
      var gameJsonUrl = "https://justbuild.nyc3.cdn.digitaloceanspaces.com/CI/1v1/Prod/162/WebGL.json"; //%gameJsonUrl
      var hostname = window.location.hostname;
      if (hostname.indexOf("dev1v1") >= 0 || hostname.indexOf("dev.1v1") >= 0 || hostname.indexOf("test1v1") >= 0 || hostname.indexOf("test.1v1") >= 0) {
        let urlParams = new URLSearchParams(window.location.search);
        let queryParam = urlParams.get("version");

        if (queryParam !== undefined && queryParam !== null) {
          gameJsonUrl = gameJsonUrl.replace(/[0-9][0-9]+/i, queryParam);
        }
      }
      var gameInstance = UnityLoader.instantiate("gameContainer", gameJsonUrl, { onProgress: UnityProgress });
      //var gameInstance = UnityLoader.instantiate("gameContainer", "Build/WebGL.json", {onProgress: UnityProgress});

      window.unityInstance = gameInstance;
      var lockedOccured = false;

      function UnityProgress(gameInstance, progress) {
        if (!gameInstance.Module) {
          return;
        }
        const loader = document.querySelector("#loader");
        if (!gameInstance.progress) {
          const progress = document.querySelector("#loader .progress");
          progress.style.display = "block";
          gameInstance.progress = progress.querySelector(".full");
          loader.querySelector(".spinner").style.display = "none";
        }
        gameInstance.progress.style.transform = `scaleX(${progress})`;
        if (progress === 1 && !gameInstance.removeTimeout) {
          loader.style.display = "none";
          gameLoaded = true;
        }
      }

      document.onkeydown = function (e) {
        if (e.altKey || e.ctrlKey || e.key == "F1" || e.key == "F2" || e.key == "F3" || e.key == "F4") {
          e.preventDefault();
        }
      };

      document.onmouseup = function (e) {
        e.preventDefault();
      };

      document.addEventListener("pointerlockchange", lockChangeAlert, false);
      document.addEventListener("mozpointerlockchange", lockChangeAlert, false);

      function lockChangeAlert() {
        if (!lockedOccured && document.pointerLockElement) lockedOccured = true;
        if (!document.pointerLockElement && lockedOccured) {
          lockedOccured = false;
          gameInstance.SendMessage("Pause Menu", "OnCursorUnlocked");
        }
      }

      window.addEventListener("resize", injectAdByWindowSize);

      function injectAdByWindowSize() {
        // Inject small ad if screen is small, or large ad if screen is large
        if (window.innerHeight < 900) {
          if (document.getElementById("adRectangleBottom") == null) {
            var el = document.getElementsByClassName("ad-rectangle-bottom")[0];
            el.id = "adRectangleBottom";
            cpmstarAPI({ kind: "go", module: "POOL 83025", config: { conditions: { target: { el: el, kind: "replace" } } } });
          }
        } else {
          if (document.getElementById("adLeaderboardBottom") == null) {
            var el = document.getElementsByClassName("ad-leaderboard-bottom")[0];
            el.id = "adLeaderboardBottom";
            cpmstarAPI({ kind: "go", module: "POOL 85420", config: { conditions: { target: { el: el, kind: "replace" } } } });
          }
        }
      }

      injectAdByWindowSize();

      var refreshNextTime = true;

      function showAds() {
        document.getElementsByClassName("ad-rectangle-bottom")[0].style.display = "block";
        document.getElementsByClassName("ad-leaderboard-bottom")[0].style.display = "block";
        document.getElementById("adRectangleUpper").style.display = "block";

        if (typeof counter === "undefined") {
          startCounter();
          resumeCounter();
        } else {
          resumeCounter();
          refresh();
        }
      }

      function hideAds() {
        document.getElementsByClassName("ad-rectangle-bottom")[0].style.display = "none";
        document.getElementsByClassName("ad-leaderboard-bottom")[0].style.display = "none";
        document.getElementById("adRectangleUpper").style.display = "none";

        pauseCounter();
      }

      // hide ads
      hideAds();

      function refresh() {
        //console.log("time since ads refresh = " + timeSinceRefresh + " seconds");
        //console.log("time ads visible = " + timeAdsVisible + " seconds");

        if (timeSinceRefresh <= 30 || timeAdsVisible <= 2) {
          //console.log("don't refresh");
          return;
        }

        if (document.getElementById("adRectangleBottom") != null && window.getComputedStyle(document.getElementsByClassName("ad-smallscreen")[0]).display != "none") {
          cpmstarAPI({ kind: "adcmd", module: "POOL 83023", command: "refresh" });
        }

        if (document.getElementById("adLeaderboardBottom") != null && window.getComputedStyle(document.getElementsByClassName("ad-largescreen")[0]).display != "none") {
          cpmstarAPI({ kind: "adcmd", module: "POOL 85420", command: "refresh" });
        }

        cpmstarAPI({ kind: "adcmd", module: "POOL 83025", command: "refresh" });

        timeSinceRefresh = 0;
        timeAdsVisible = 0;
        //console.log("refresh ads");
      }

      window.onfocus = function () {
        //console.log("onfocus");
        resumeCounter();
        refresh();
      };

      window.onblur = function () {
        //console.log("onblur");
        pauseCounter();
      };

      var timeSinceRefresh = 0;
      var timeAdsVisible = 0;
      var counter;
      var adsVisible = false;

      function startCounter() {
        timeSinceRefresh++;
        if (adsVisible) timeAdsVisible++;

        counter = setTimeout(function () {
          startCounter();
        }, 1000);
      }

      function resumeCounter() {
        adsVisible = true;
      }

      function pauseCounter() {
        adsVisible = false;
      }
    </script>
    <!-- Firebase App (the core Firebase SDK) is always required and must be listed first -->
    <script src="firebase/firebase-app.js"></script>

    <!-- Add Firebase products that you want to use -->
    <script src="firebase/firebase-analytics.js"></script>
    <script src="firebase/firebase-auth.js"></script>
    <script src="firebase/firebase-firestore.js"></script>
    <script src="firebase/firebase-remote-config.js"></script>

    <script src="js/firebase.js?v=147"></script>
    <script src="js/login.js?v=147"></script>
    <script src="js/firebase-config.js?v=147"></script>

    <script>
      var hostname = window.location.hostname;
      if (hostname.indexOf("dev1v1") >= 0 || hostname.indexOf("dev.1v1") >= 0 || hostname.indexOf("test1v1") >= 0 || hostname.indexOf("test.1v1") >= 0 || hostname.indexOf("localhost") >= 0) {
        initializeFireBaseDev();
      } else {
        initializeFireBase();
      }

      initRemoteConfig();
    </script>

    <script src="js/windowResize.js"></script>
    <script src="js/adblockManager.js"></script>
    <script src="js/macUserAgent.js"></script>
    <script src="js/visibilityChangeListener.js"></script>
    <script>
      function onUnityReady() {
        checkAdBlock();
        sendConfig();
      }

      fixMacUserAgent();
    </script>
    <script src="/js/main.js"></script>
  </body>
</html>
