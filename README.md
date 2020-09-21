package com.example.ff;

import android.net.Uri;

import java.io.IOException;
import java.io.InputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Scanner;
//////////////////////////////CONNECTION....................................
public class Connect {
    private static String API = "http//172.56.14:45560/api/";

    public static URL getURL(String f)
    {
        Uri uri = Uri.parse(API +f).buildUpon().build();
        URL url = null;
        //url = new URL(uri.toString());
        try {
            url = new URL(uri.toString());
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
        return url;
    }

    public static String getResponseFromUrl (URL url) throws IOException
    {
        HttpURLConnection httpURLConnection = (HttpURLConnection)url.openConnection();
        try {
            InputStream in = httpURLConnection.getInputStream();
            Scanner scanner = new Scanner(in);
            scanner.useDelimiter("\\A");
if (scanner.hasNext())
{
    return scanner.next();
}
else return null;

        }
        finally {
            httpURLConnection.disconnect();
        }
    }

}
/////////////////----АВТОРИЗАЦИЯ..........................................................
package com.example.ff;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.AsyncTask;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.io.IOException;
import java.net.URL;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

import android.os.AsyncTask;
import android.os.Bundle;

import static com.example.ff.Connect.getResponseFromUrl;
import static com.example.ff.Connect.getURL;

public class autorization extends AppCompatActivity {

    class AT extends AsyncTask <URL, Void, String>
    {

        @Override
        protected String doInBackground(URL... urls) {
            String response = null;
            try {
                response = getResponseFromUrl(urls[0]);
            } catch (IOException e) {
                e.printStackTrace();
            }
            return response;
        }

        @Override
        protected void onPostExecute(String s) {
            super.onPostExecute(s);
            try {
                JSONArray jsonArray = new JSONArray(s);
                for (int i=0; i<s.length();i++)
                {
                    JSONObject jsonObject = jsonArray.getJSONObject(i);
                    String s1 = jsonObject.getString("Controller");

                }

            } catch (JSONException e) {
                e.printStackTrace();
            }
        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_autorization);
        new AT().execute(getURL("Controller"));
    }
}
?//////////// EVENT//////////////////////////////
package com.example.ff;

public class Event {
    public String getP1() {
        return p1;
    }

    public void setP1(String p1) {
        this.p1 = p1;
    }

    public String getP2() {
        return p2;
    }

    public void setP2(String p2) {
        this.p2 = p2;
    }

    private String p1;
    private String p2;

    public Event(String p1,String p2)
    {
        this.p1 = p1;
        this.p2 = p2;
    }
}
//////////////EventAdapter
package com.example.ff;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;

import java.util.List;

public class EventAdapter extends ArrayAdapter {
private int anInt;
private List<Event> events;
LayoutInflater inflater;

    public EventAdapter(@NonNull Context context, int resource, @NonNull List <Event> events) {
        super(context, resource, events);
        this.anInt = resource;
        this.events = events;
        this.inflater = LayoutInflater.from(context);
    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        View view = inflater.inflate(anInt, parent, false);
        TextView textView = (TextView)view.findViewById(R.id.test1);
        Event event = events.get(position);
        textView.setText(event.getP1()+event.getP2());
        return view;
    }

}
////////////////////////////////ОТКРЫТИЕ
public void OnClick1 (View view)
    {
        Intent intent = new Intent(MainActivity.this,autorization.class);
        startActivity(intent);
        
    }
//писать в валуес кнтролер 
[Route("api/ADDUsersssses/{id}")]
        public string  GetADDUserssssess(string id)
        {
            string[] userss = id.Split('=');

            Person person1 = new Person();

            person1.ID_person = db.Person.Max(r => r.ID_person) + 1;
            person1.s_firstname = userss[0];
            person1.s_lastname = userss[1];
            person1.s_patrinymic = userss[2];
            person1.s_phone = userss[3];
            db.Person.Add(person1);
            db.SaveChanges();
}
.////////////// строка в браузере имеет вид имеет вид
https://192.168.1.206:44341/api/ADDUsersssses/firstame=lastname=pat=phone
