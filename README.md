# ziyong
# youtube去广告
#!name=去除 Youtube 广告 
#!desc=去除 Youtube 广告（Beta）
# 请勿与其他YouTube模块一起使用IOS > 15
# 删除 瀑布流、视频、搜索中出现的广告和Shorts，
# 删除 Shorts 内的视频广告
# 删除 底部 上传 按钮
# 广告信息可能有遗漏，可能偶现广告
# inspired by @Choler & @DivineEngine & @app2smile

[URL Rewrite]
# 使用 Mock 减少开销
^https?:\/\/[\w-]+\.googlevideo\.com\/initplayback.+&oad - reject-dict

[Script]
# 该模块已足够全面，无需其他规则混用，防止重写规则被破坏。https:\/\/youtubei\.googleapis\.com\/youtubei\/v1\/(browse|next|player|search|reel\/reel_watch_sequence|guide),requires-body=1,binary-body-mode=1,max-size=3145728,script-path=https://raw.githubusercontent.com/Maasea/sgmodule/master/Script/Youtube/youtube.js
youtube-proto = type=http-response,pattern=^https:\/\/youtubei\.googleapis\.com\/youtubei\/v1\/(browse|next|player|search|reel\/reel_watch_sequence|guide),requires-body=1,binary-body-mode=1,max-size=3145728,script-path=https://raw.githubusercontent.com/Maasea/sgmodule/master/Script/Youtube/youtube.js


[MITM]
hostname = %APPEND% *.googlevideo.com, youtubei.googleapis.com
