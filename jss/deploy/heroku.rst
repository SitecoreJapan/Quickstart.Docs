#####################################
heroku へ展開する
#####################################


yarn 削除

heroku logs --tail
git push -u heroku master
git push heroku master
heroku create sitecorejp
npm install
npm start
