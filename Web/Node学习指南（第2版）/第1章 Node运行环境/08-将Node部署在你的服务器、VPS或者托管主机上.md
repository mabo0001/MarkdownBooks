[toc]

### 1.3.1　将 Node 部署在你的服务器、VPS 或者托管主机上

把 Node 应用部署在和 WordPress 一样的机器上是行不通的，因为 Node 有特殊的权限需求。虽然没有 root 或管理权限也可以运行 Node，但最好有。此外，许多托管公司并不喜欢让你在多个端口上托管（host）应用，不论它会不会对其系统造成破坏。

在虚拟专用服务器（VPS）（例如我在 Linode 上的 VPN ）上部署 Node，是一件很简单的事情。你的 VPS 具有 root 访问权限，只要你不危及可能位于同一机器上的其他用户，就可以做任何操作。提供 VPS 的大多数公司都能确保每个个人账户与其他账户隔离，也没有任何一个账户能够占用所有可用的资源。

但是，使用 VPS 的问题与你使用自己的服务器时所遇到的问题相同：你必须维护服务器，包括设置电子邮件系统和别的 Web 服务器——通常是 Apache 或 Nginx ——来处理防火墙、其他安全性问题以及电子邮件等。这可不是小问题。

不过，如果你有能力全面地管理一个互联网主机，VPS 足以用来部署 Node 程序了。在你准备好将程序部署到产品环境之前，你可能会想要了解一下如何在云端环境部署应用程序。

