# hello
Messages 
echo -e "Installing legacy WhatsApp 2.11.431"
if [ $sdkver -ge 17 ]; then
adb install -r -d tmp/LegacyWhatsApp.apk
else
adb install -r tmp/LegacyWhatsApp.apk
fi
echo -e "Install complete\n"
if [ $sdkver -ge 23 ]; then
adb backup -f tmp/whatsapp.ab com.whatsapp
else
adb backup -f tmp/whatsapp.ab -noapk com.whatsapp
fi
if [ -f tmp/whatsapp.ab ]; then
echo -e "\nPlease enter your backup password (leave blank for none) and press Enter: "
read password
java -jar bin/abe.jar unpack tmp/whatsapp.ab tmp/whatsapp.tar $password
tar xvf tmp/whatsapp.tar -C tmp apps/com.whatsapp/f/key
tar xvf tmp/whatsapp.tar -C tmp apps/com.whatsapp/db/msgstore.db
tar xvf tmp/whatsapp.tar -C tmp apps/com.whatsapp/db/wa.db
tar xvf tmp/whatsapp.tar -C tmp apps/com.whatsapp/db/axolotl.db
tar xvf tmp/whatsapp.tar -C tmp apps/com.whatsapp/db/chatsettings.db
echo -e "\nSaving whatsapp.cryptkey ..."
cp tmp/apps/com.whatsapp/f/key extracted/whatsapp.cryptkey
