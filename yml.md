
# FILE: webapp.yml
# Location: ~/ansible-webapp/webapp.yml

---
- name: Deploy a Simple Web Application
  hosts: localhost
  connection: local
  become: true

  tasks:

    - name: Install Apache web server
      ansible.builtin.apt:
        name: apache2
        state: present
        update_cache: true

    - name: Start and enable Apache
      ansible.builtin.service:
        name: apache2
        state: started
        enabled: true

    - name: Deploy the web application
      ansible.builtin.copy:
        dest: /var/www/html/index.html
        content: |
          <!DOCTYPE html>
          <html>
          <head>
              <title>My Ansible Web App</title>
          </head>
          <body>
              <h1>Hello from Ansible!</h1>
              <p>My web application was deployed automatically.</p>
          </body>
          </html>
        mode: "0644"

    - name: Verify the web application
      ansible.builtin.uri:
        url: http://127.0.0.1/
        status_code: 200
      register: web_result

    - name: Display deployment status
      ansible.builtin.debug:
        msg: "Web application deployed successfully!"
