# ziyong
# ------------------
# 整体的圈X配置根据各位大佬文件修改（完全自用备份）
# 修改日期:2022年11月15日
# ⚠️注意⚠️: 以下内容中，带“;” “#”的都是注释符号，去掉前面的符号，该行才有效
# ------------------
# 最新完整的示例需查看 Quantumult X 里「配置文件」中的「示例」

[general]
# 建议在「其他设置」里「GeoLite2」的「来源」填写使用「 https://cdn.jsdelivr.net/gh/Hackl0us/GeoIP2-CN@release/Country.mmdb 」并开启「自动更新」

;profile_img_url=http://www.example.com/example.png

# resource_parser_url 示例可以在以下网站找到 https://raw.githubusercontent.com/crossutility/Quantumult-X/master/resource-parser.js
# 资源解析器
resource_parser_url=https://cdn.jsdelivr.net/gh/KOP-XIAO/QuantumultX@master/Scripts/resource-parser.js

# geo_location_checker
# 用于节点页面的信息展示，可完整自定义
# geo_location_checker=disabled
geo_location_checker=http://ip-api.com/json/?lang=zh-CN, https://raw.githubusercontent.com/I-am-R-E/Functional-Store-Hub/Master/GeoLocationChecker/QuantumultX/IP-API.js

# Quantumult 使用 HEAD 方法将 HTTP 请求发送到服务器检查 url 来测试代理的状态，结果应该是两个延迟，第一个是 TCP 与代理服务器的握手，第二个是 Quantumult 成功地从服务器检查 url 接收 HTTP 响应的总时间。闪电图标表示 TCP Fast Open 成功。如果 [server_local] 或 [server_remote] 中的服务器有自己的 server_check_url，则会用自己的 server_check_url 代替 [general] 中的 server_check_url。
# Quantumult 使用 HTTP HEAD 方法对测试网址 server_check_url 进行网页响应性测试(测试结果为通过该节点访问此网页获得 HTTP 响应所需要的时间)，来确认节点的可用性。
# Quantumult 界面中的延迟测试方式均为网页响应性测试，显示的最终延迟均为通过对应节点访问测试网页获得 HTTP 响应所需要时间。
# 由于 Trojan 协议为无响应校验协议，使得 HTTP 检测方式即使获得了 HTTP 响应，也不代表节点一定可用。
server_check_url=http://cp.cloudflare.com/generate_204

# DNS 排除列表
# dns_exclusion_list 包含了禁用占位符 IP (240.*) 的域，不在 dns_exclusion_list 中的域都启用了占位符 IP，并打开了 resolve-on-remote 设置。
dns_exclusion_list=*.cmpassport.com, *.jegotrip.com.cn, *.icitymobile.mobi, id6.me

# Quantumult 将不会处理到 excluded_routes 的流量。修改后最好重新启动您的设备。
;excluded_routes=192.168.0.0/16, 172.16.0.0/12, 100.64.0.0/10, 10.0.0.0/8
# Hearthstone: 24.105.30.129/32, 185.60.112.157/32, 185.60.112.158/32, 182.162.132.1/32
excluded_routes=239.255.255.250/32

# 在网络环境切换时出发运行模式变更
# filter - 规则分流
# all_proxy - 全部代理
# all_direct - 全部直连
# 示例意思：[蜂窝数据],[Wi-Fi],[SSID]
# 下列示例的意思为：
# 在蜂窝数据使用规则分流(第一个 filter)
# 在 Wi-Fi 使用规则分流(第二个 filter)
# 在SSID为 LINK_22E171 的Wi-Fi使用全部代理
# 在SSID为 LINK_22E172 的Wi-Fi使用全部直连
;running_mode_trigger=filter, filter, LINK_22E171:all_proxy, LINK_22E172:all_direct

# 在特定 SSID 网络时(除了 Task 模块)暂停 Quantumult X
;ssid_suspended_list=LINK_22E174, LINK_22E175

# 参数 udp_whitelist 从 IP 层控制 UDP 数据是否需要舍弃；如舍弃，则该 UDP 请求不会进入规则模块以及策略模块，TCP/UDP 请求记录中也不会有相应的条目，但仍可在日志中查询到相关信息（日志等级 debug）。
# 该参数控制的是流入 Quantumult X Tunnel 的请求，并非 Quantumult X Tunnel 发出的请求，即不会作用于节点所使用的 UDP 目标端口。
;udp_whitelist=53, 123, 1900, 80-443
udp_whitelist=1-442, 444-65535

# 说明：参数 fallback_udp_policy 的值仅支持末端策略（末端策略为经由规则模块和策略模块后所命中的策略，例如：direct、reject 以及节点；不支持内置策略 proxy 以及其它自定义策略）。默认为 reject。
# 当 UDP 请求经过规则模块以及策略模块后所命中的节点为 Quantumult X 所不支持 UDP 转发的节点（如：VMess、trojan），或支持 UDP 转发但未注明 udp-relay=true 的（例如：SS/SSR 且与服务器是否真实开启 UDP 转发无关），则 fallback_udp_policy 会被使用。
# 注意：如果您需要调整该参数的值为 direct，请务必清楚了解同一目标主机名 TCP 请求与 UDP 请求的源地址不同所造成的隐私及安全风险。
# 如果没有节点支持 UDP 转发，可取消下条注释（去除 ;）
;fallback_udp_policy=direct

;icmp_auto_reply=true

[dns]
# 查询结果只用于评估过滤器或通过直接策略连接，当通过服务器连接时，查询结果不会被使用，Quantumult 永远不会知道相关域名的目标 IP。
# 如果您想让某个域名(例如：example.com)为 127.0.0.0.1，只需在「filter_local」部分添加「host, example.com, reject」即可。拒绝操作将返回 127.0.0.0.1 的 DNS 响应。

# 禁用系统 DNS
# 为了提高性能，会使用从当前网络(系统)中获取的 DNS 服务器(您可以使用「no-system」禁用此功能，但至少要增加一个自定义的 DNS 服务器。
;no-system

# 禁用 IPv6
# 当设置「no-ipv6」时，Quanumult X Tunnel 的 DNS 模块会直接让 AAAA 查询失败。
no-ipv6

# 自定义 DNS
# > OneDNS
;server=117.50.10.10
# > DNSPod Public DNS
server=119.29.29.29
# > Alibaba Public DNS
server=223.5.5.5

# 在特定的网络环境下忽略自定义 DNS 可在后方加上「excluded_ssids」相关字段。
# 注意：如配置了 no-system，则请务必确保在忽略了部分自定义 DNS 的配置下至少有一个可用的自定义 DNS 配置。
# server=114.114.114.114, excluded_ssids=SSID1, SSID2

# DNS over HTTPS
# 当 DoH 服务器被设置时，所有其他普通的（没有与之相关的特定域）服务器将被忽略。
# 当设置了多个 DoH 服务器时，只有第一个会被使用。
# 当使用的 DoH 服务器不是基于 HTTP/2 时，DoH 将被暂时禁用，并使用常规服务器，直到下次启动 VPN 连接。
# 不建议在与防火墙相关的网络环境中使用，不确定 DoH 服务器是否总能被到达。
# 如果 DoH 服务器在您的国家或地区不是流行的 DNS 服务器，则不推荐使用，它可能会丢失 ISP DNS 服务器返回的 CDN 优化结果。
# 如果 DoH 服务器是一个反广告相关的服务器，则不推荐使用（Quantumult X 过滤模块对于被拒绝的域具有更好的性能，它可以避免客户端无休止的请求）。
;doh-server=https://dns.alidns.com/dns-query
;doh-server=https://223.6.6.6/dns-query

# 本地 DNS 映射

# > Firebase Cloud Messaging
address=/mtalk.google.com/108.177.125.188
# > Google Dl
server=/dl.google.com/119.29.29.29
server=/dl.l.google.com/119.29.29.29
server=/update.googleapis.com/119.29.29.29

# > PlayStation
server=/*.dl.playstation.net/119.29.29.29

# > Router Admin Panel
server=/amplifi.lan/system
server=/router.synology.com/system
server=/sila.razer.com/system
server=/router.asus.com/system
server=/routerlogin.net/system
server=/orbilogin.com/system
server=/www.LinksysSmartWiFi.com/system
server=/LinksysSmartWiFi.com/system
server=/myrouter.local/system
server=/www.miwifi.com/system
server=/miwifi.com/system
server=/mediarouter.home/system
server=/tplogin.cn/system
server=/tplinklogin.net/system
server=/melogin.cn/system
server=/falogin.cn/system

;server=8.8.4.4:53
;server=/example0.com/system
;server=/example1.com/8.8.4.4
;server=/*.example2.com/223.5.5.5
;server=/example4.com/[2001:4860:4860::8888]:53
;address=/example5.com/192.168.16.18
;address=/example6.com/[2001:8d3:8d3:8d3:8d3:8d3:8d3:8d3]

[policy]

url-latency-benchmark=优选节点, server-tag-regex=.*?, check-interval=1800, tolerance=0, alive-checking=false, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/VIP.png
url-latency-benchmark=美国节点, server-tag-regex=US|美国|🇺🇸, check-interval=600, tolerance=0, alive-checking=false, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/United_States.png
url-latency-benchmark=日本节点, server-tag-regex=日|日本|JP|🇯🇵, check-interval=600, tolerance=0, alive-checking=false, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Japan.png
url-latency-benchmark=香港节点, server-tag-regex=港|香港|HK|🇭🇰, check-interval=600, tolerance=0, alive-checking=false, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Hong_Kong.png
url-latency-benchmark=台湾节点, server-tag-regex=台|台湾|TW|🇨🇳, check-interval=600, tolerance=0, alive-checking=false, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Taiwan.png
# 分流策略组板块
# 需要策略图标的在策略后加上：img-url=http://example.com/icon.png

# 类型：静态(static)
# 指向您手动选择的候选服务器。
;static=policy-name-1, Sample-A, Sample-B, Sample-C, img-url=http://example.com/icon.png

# 类型：可用(available)
# 指向候选服务器的第一个可用服务器(当策略被触发且策略结果不可用时，将立即启动并发 url 延迟测试。
# 如果当时没有网络请求接受策略，这意味着策略处于空闲状态，即使服务器关闭，测试也不会启动。那时，您可以通过手动启动测试来更新服务器状态，但是这没有任何意义)。
;available=policy-name-2, Sample-A, Sample-B, Sample-C

# 类型：负载均衡(round-robin)
# 指向在候选服务器中指向下一个服务器以进行下一次连接。
;round-robin=policy-name-3, Sample-A, Sample-B, Sample-C

# 类型：延迟测试(url-latency-benchmark)
# 策略指向具有最佳 URL 延迟(公差，单位毫秒)结果的服务器。
# 当用户在 Quantumult X 中手动启动 URL 测试时，策略结果也会被更新。
# 该类型的策略有一个名为 check-interval(秒) 的参数，如果此策略已经被任何请求激活，则将考虑该间隔。
;url-latency-benchmark=policy-name-8, resource-tag-regex=^sample, server-tag-regex=^example, check-interval=600, tolerance=0

# SSID
# 策略根据网络环境的不同指向服务器。
;ssid=policy-name-4, Sample-A, Sample-B, LINK_22E171:Sample-B, LINK_22E172:Sample-C

# resource-tag-regex 及 server-tag-regex 仅适用于 static、available 和 round-robin 类型的策略。
;static=policy-name-5, resource-tag-regex=^sample, server-tag-regex=^example, img-url=http://example.com/icon.png
;available=policy-name-6, resource-tag-regex=^sample, server-tag-regex=^example
;round-robin=policy-name-7, resource-tag-regex=^sample, server-tag-regex=^example
# 以下前两行节点筛选策略组为示范使用，请根据自身情况自行修改正则表达式
# 分流策略组
static=油管视频, 优选节点, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/YouTube.png
static=电报社交, 优选节点, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Telegram.png
static=网络测速, 美国节点, 日本节点, 台湾节点, 香港节点, direct, proxy, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Speedtest.png
static=TikTok, 美国节点, 日本节点, 台湾节点, direct, proxy, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/TikTok_1.png
static=字节跳动, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/TikTok.png
static=全球加速, 优选节点, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Global.png
static=声田音乐, 美国节点, 日本节点, 香港节点, 台湾节点, proxy, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Spotify.png
static=迪士尼影视, 美国节点, 日本节点, 香港节点, 台湾节点, direct, proxy, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Disney.png
static=国际媒体, 优选节点, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/ForeignMedia.png
static=哔哩哔哩, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/bilibili_2.png
static=推特社交, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Twitter.png
static=苹果服务, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Apple.png
static=谷歌服务, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Google_Search.png
static=微软服务, direct, 美国节点, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Windows_11.png

static=新浪微博, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Weibo.png
static=广告拦截, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Advertising.png
static=中国大陆, proxy, direct, reject, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/China_Map.png
static=分流兜底, 美国节点, 日本节点, 台湾节点, 香港节点, proxy, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Final.png

[server_remote]

#添加节点



[filter_remote]
# 分流规则板块
# 参数「tag」、「force-policy」和「enabled」是可选的。
# 当有强制策略时，远程资源的过滤器中的策略将被忽略，并使用强制策略。
# 隐藏真实IP分流规则

# Speedtest测速
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Speedtest/Speedtest.list, tag=Speedtest, force-policy=网络测速, update-interval=172800, opt-parser=true, enabled=true

# Unbreak 后续规则修正
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Surge/Ruleset/Unbreak.list, tag=后续规则修正, force-policy=direct, update-interval=172800, opt-parser=true, enabled=true

# Hijacking 运营商劫持或恶意网站
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Surge/Ruleset/Guard/Hijacking.list, tag=运营商劫持或恶意网站, force-policy=reject, update-interval=172800, opt-parser=true, enabled=true
#隐私保护
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Surge/Ruleset/Guard/Privacy.list, tag=隐私保护, force-policy=reject, update-interval=172800, opt-parser=true, enabled=true
# Advertising去广告
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Advertising/Advertising.list, tag=Advertising, force-policy=广告拦截, update-interval=86400, opt-parser=true, enabled=true

# 字节跳动规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/ByteDance/ByteDance.list, tag=字节跳动, force-policy=字节跳动, update-interval=86400, opt-parser=true, enabled=true

# YouTube规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX//YouTube/YouTube.list, tag=YouTube, force-policy=油管视频, update-interval=86400, opt-parser=false, enabled=true
# Spotify规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Spotify/Spotify.list, tag=声田音乐 规则, force-policy=声田音乐, update-interval=86400, opt-parser=false, enabled=true
# Disney规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Disney/Disney.list, tag=Disney, force-policy=迪士尼影视, update-interval=172800, opt-parser=true, enabled=true
#toktok
https://raw.githubusercontent.com/Semporia/TikTok-Unlock/master/Quantumult-X/TikTok.list, tag=TikTok, force-policy=TikTok, update-interval=86400, opt-parser=false, enabled=true
# 国际媒体规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/GlobalMedia/GlobalMedia.list, tag=国际媒体, force-policy=国际媒体, update-interval=86400, opt-parser=false, enabled=true
# Telegram规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Telegram/Telegram.list, tag=Telegram, force-policy=电报社交, update-interval=86400, opt-parser=false, enabled=true

# Twitter规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Twitter/Twitter.list, tag=Twitter, force-policy=推特社交, update-interval=86400, opt-parser=false, enabled=true
# Google规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Google/Google.list, tag=Google, force-policy=谷歌服务, update-interval=86400, opt-parser=false, enabled=true
# Apple规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Apple/Apple.list, tag=Apple, force-policy=苹果服务, update-interval=86400, opt-parser=true, enabled=true
# 全球加速规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/release/rule/QuantumultX/Global/Global.list, tag=全球加速, force-policy=全球加速, update-interval=86400, opt-parser=false, enabled=true
# BiliBili规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/BiliBili/BiliBili.list, tag=Bilibili, force-policy=哔哩哔哩, update-interval=86400, opt-parser=false, enabled=true
# Microsoft规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Microsoft/Microsoft.list, tag=微软服务, force-policy=微软服务, update-interval=86400, opt-parser=false, enabled=true
# 中国大陆规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/China/China.list, tag=中国大陆, force-policy=中国大陆, update-interval=86400, opt-parser=false, enabled=true

[rewrite_remote]
# 远程重写订阅板块
# 参数「tag」和「enabled」是可选的。
#youtube去广告
https://raw.githubusercontent.com/Maasea/sgmodule/master/youtubePlayer.sgmodule, tag=yutube去贴片广告, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/app2smile/rules/master/module/youtube-qx.conf, tag=youtube首页瀑布流广告, update-interval=172800, opt-parser=true, enabled=true
# General
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/General.conf, tag=General, update-interval=172800, opt-parser=false, enabled=true

# Block Advertising
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/Advertising.conf, tag=Block Advertising, update-interval=172800, opt-parser=false, enabled=true

# Block Advertising+
https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/AdvertisingPlus.conf, tag=Block Advertising+, update-interval=172800, opt-parser=false, enabled=true

# 去广告分流规则
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/release/rewrite/QuantumultX/Advertising/Advertising.conf, tag=Advertising, update-interval=86400, opt-parser=false, enabled=true

# 解锁酷我超级VIP
https://raw.githubusercontent.com/nameking77/Qx/main/rewrite/kw.js, tag=酷我超级VIP, update-interval=172800, opt-parser=true, enabled=true

# P站去广告

# 多合一去广告
https://raw.githubusercontent.com/erdongchanyo/Rules/main/Quantumult%20X/AllinOneRewrite/edc.conf, tag=多合一去广告, update-interval=86400, opt-parser=true, enabled=true

# Redirect重定向
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rewrite/QuantumultX/Redirect/Redirect.conf, tag=Redirect重定向, update-interval=86400, opt-parser=false, enabled=true

# Apple定位
https://raw.githubusercontent.com/VirgilClyne/iRingo/main/qxrewrite/Location.qxrewrite, tag=Apple定位, update-interval=86400, opt-parser=true, enabled=true

# Siri与搜索
https://raw.githubusercontent.com/VirgilClyne/iRingo/main/qxrewrite/Siri.qxrewrite, tag=Siri与搜索, update-interval=86400, opt-parser=false, enabled=true

#微信解锁屏蔽URL
https://raw.githubusercontent.com/zZPiglet/Task/master/UnblockURLinWeChat.conf, tag=微信解锁被屏蔽的URL

#油管字幕翻译
https://raw.githubusercontent.com/id77/QuantumultX/master/rewrite/Youtube_CC.conf#out=Hant, tag=油管字幕翻译, update-interval=172800, opt-parser=false, enabled=true
#小帽重写
#小帽重写1-整合 - 去广告 解锁脚本 等
https://raw.githubusercontent.com/xiaomaoJT/QX_Script/main/rewrite/xiaomao/QuantumultX_XiaoMao_rw1.conf, tag=XiaoMao-rewrite-01-other, update-interval=172800, opt-parser=false, enabled=true
#小帽重写 开屏广告 c-墨鱼 z-张军
https://gitlab.com/ddgksf2013/Cuttlefish/-/raw/master/Rewrite/AdBlock/StartUp.conf, tag=XiaoMao-开屏广告-C, update-interval=172800, opt-parser=false, enabled=true
#去广告重写
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rewrite/QuantumultX/Advertising/Advertising.conf, tag=XiaoMao-去广告正式, update-interval=172800, opt-parser=false, enabled=true

[server_local]
# 本地节点板块
# 只有 obfs=http, obfs=ws, obfs=ws, obfs=wss 可以有可选的「obfs-uri」字段。
# wss 中的 obfs-host 参数将用于 TLS 握手和 HTTP 头主机字段，如果没有为 wss 设置 obfs-host，则将使用服务器地址。
# 目前不支持 VMess 和 Trojan 的 UDP relay。
# 当使用 obfs=ws 和 obfs=wss 时，服务器端可以通过带有 mux=0 的 v2ray-plugin 或 v2ray-core 进行部署。
# obfs plugin tls1.2 ticket auth 比 tls1.2 ticket fastauth 和 obfs tls 多一个 RTT，你最好使用 tls1.2 ticket fastauth。
# chacha20-ietf-poly1305 和 chacha20-poly1305 在 VMess 配置中具有相同的效果。

# 可选字段 tls13 仅用于：shadowsocks obfs=wss / vmess obfs=over-tls and obfs=wss / http over-tls=true / trojan over-tls=true
# [server_local] 完整示例请查看「示例」

[filter_local]
# 本地分流规则:相同规则下本地规则优先生效
host-keyword, ugreen, direct
# > 字节跳动
HOST-SUFFIX,pangolin-sdk-toutiao.com, reject
HOST-SUFFIX,pangolin-sdk-toutiao-b.com, reject
HOST-SUFFIX,api-access.pangolin-sdk-toutiao-b.com, reject
HOST,ad.toutiao.com, reject
HOST,dsp.toutiao.com, reject
host-keyword,pangolin.snssdk.com, reject
# 绕过企业证书过期
host, ocsp.apple.com, reject

# 其它
host-suffix, local, direct
ip-cidr, 192.168.0.0/16, direct
ip-cidr, 10.0.0.0/8, direct
ip-cidr, 172.16.0.0/12, direct
ip-cidr, 127.0.0.0/8, direct
ip-cidr, 100.64.0.0/10, direct
ip-cidr, 224.0.0.0/4, direct
ip6-cidr, fe80::/10, direct
ip-cidr, 203.107.1.1/24, reject
ip-cidr, 183.240.197.130/32, direct
#微信转圈
ip-asn, 132203, direct

geoip, cn,中国大陆
final,分流兜底

[rewrite_local]
# 本地重写板块
# [rewrite_local] 完整示例请查看「示例」

# Sub-Store 需要mitm (sub.store)

^https?:\/\/sub\.store\/((download)|api\/(preview|sync|(utils\/node-info))) url script-analyze-echo-response https://github.com/sub-store-org/Sub-Store/releases/latest/download/sub-store-1.min.js
^https?:\/\/sub\.store url script-analyze-echo-response https://github.com/sub-store-org/Sub-Store/releases/latest/download/sub-store-0.min.js

#解锁百度会员   需要mitm  (pan.baidu.com)
^https:\/\/pan\.baidu\.com\/rest\/\d\.\d\/membership\/user url script-response-body https://raw.githubusercontent.com/NobyDa/Script/master/Surge/JS/BaiduCloud.js

#spotify 需要mitm (spclient.wg.spotify.com)
^https:\/\/spclient\.wg\.spotify\.com\/(bootstrap\/v1\/bootstrap|user-customization-service\/v1\/customize)$ url script-response-body https://raw.githubusercontent.com/app2smile/rules/master/js/spotify-proto.js

#Tiktok解锁，需要mitm (hostname = *.tiktokv.com, *.byteoversea.com, *.tik-tokapi.com)
(?<=_region=)CN(?=&) url 307 KR
(?<=&mcc_mnc=)4 url 307 2
^(https?:\/\/(tnc|dm)[\w-]+\.\w+\.com\/.+)(\?)(.+) url 302  $1$3
(?<=\d\/\?\w{7}_\w{4}=)1[6-9]..(?=.?.?&) url 307 17
#tiktok换区，将下列CN改为想看的国家/地区的2位大写英文简写 JP（日本）｜KR（韩国）｜UK（英国）｜US（美国）｜TW（台湾）
(?<=_region=)TW(?=&) url 307 TW
[task_local]
# $task.fetch() 组成一个 HTTP 请求并处理响应，只支持 text body。如果您想要 serial requests 而不是 current requests，可以将 $task.fetch() 嵌入到另一个 $task.fetch() 的完成处理程序中。
#
# 脚本应保存在本地「我的 iPhone - Quantumult X - Scripts」或「iCloud Drive - Quantumult X - Scripts」中。示例：https://github.com/crossutility/Quantumult-X/blob/master/sample-task.js
#
# 默认的 HTTP 请求超时是 10 秒。
#
# 支持 5 或 6 个 cron 字段，不包括命令字段。
#
# [task_local] 完整示例请查看「示例」
event-interaction https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/ytb-ui-check.js, tag=YouTube 查询, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/YouTube_Letter.png, enabled=true
event-interaction https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/geo_location.js, tag=GeoIP 查询, img-url=location.fill.viewfinder.system, enabled=true
event-interaction https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/switch-check-google.js, tag=Google送中检测, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Google.png, enabled=true
# 清理DNS缓存
0 0/6 * * ? https://raw.githubusercontent.com/unknowntokyo/surge-list/master/X/dns-clear-cache.js, tag=清理DNS缓存, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Lab.png, enabled=true

event-interaction https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/streaming-ui-check.js, tag=流媒体服务查询, img-url=checkmark.seal.system, enabled=true


[http_backend]
#
# 部署一个本地 HTTP 服务器，并使用 JavaScript 进行数据处理。
# 输入变量为：$reqeust.url、$reqeust.path、$reqeust.headers、$reqeust.body。
# 使用 $done 输出像 $done({status:"HTTP/1.1 200 OK"}, headers:{}, body:"here is a string") 这样的返回响应。
# 此外，您还可以使用签名或任何其他验证方法来验证请求是否合法。
# 部署后您应该通过 http://127.0.0.1:9999/your-path/your-api/. 进行访问。服务器默认监听端口为 9999，您可以在UI中进行更改。
#
# [http_backend] 完整示例请查看「示例」

[mitm]
passphrase = F741A08D
p12 = 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
# 只有「hostname」中的 TLS SNI 或目标地址将被 MitM 处理。
#
# 默认情况下，当为 HTTPS 请求启用 MitM 时，Quantumult X 会从原站点获取证书（证书会被缓存），保留大部分需要的原始证书信息，并使用 MitM 的 root CA 重新签名，这是推荐的（也是比较兼容的）MitM 证书创建方式。
#
# 偶尔有些用户喜欢调试 HTTPS 请求，其域名不存在，所以原证书根本不存在。当参数 simple_cert_hostname 出现的时候。其 TLS SNI 名称在 simple_cert_hostname(及 hostname) 中的 HTTPS 请求将使用纯本地生成的 MitM 证书。
#
# 注意！！！您应该始终保护您的 CA 密码和 p12 的私密性。
#
;passphrase =
;p12 =
skip_validating_cert = true
;force_sni_domain_name = false
;simple_cert_hostname = non-existed-domain.com, *.non-connected-domain.com
